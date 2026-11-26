<template>
  <div class="max-w-4xl mx-auto p-4 sm:p-8 space-y-6">
    <h1 class="text-2xl font-bold">Buff Like — chaysk.com</h1>
    <p class="text-sm text-stone-600">Nhập đúng tên nhân vật. Đơn được xếp hàng và tự chuyển về PC khi máy nhận đơn hoạt động.</p>
    <form @submit.prevent="submit" class="bg-white border rounded-2xl p-5 space-y-4">
      <label class="block text-sm">Gói dịch vụ
        <select v-model="productId" required class="block w-full border rounded-lg p-2 mt-1" :disabled="busy">
          <option value="" disabled>Chọn gói buff like</option>
          <option v-for="p in products" :key="p.id" :value="p.id">{{ p.name }} — {{ p.likesPerItem }} like / gói — {{ formatVND(p.price) }}</option>
        </select>
      </label>
      <p v-if="!products.length" class="text-amber-700 text-sm">Chưa có gói buff like. Admin cần tạo sản phẩm loại Buff Like (PC).</p>
      <label class="block text-sm">Tên nhân vật
        <input v-model="targetName" required maxlength="100" :disabled="busy" class="block w-full border rounded-lg p-2 mt-1" />
      </label>
      <label class="block text-sm">Số gói
        <input v-model.number="quantity" type="number" :min="selected?.minQuantity || 1" :max="selected?.maxQuantity || 1" required :disabled="busy" class="block w-full border rounded-lg p-2 mt-1" />
      </label>
      <p class="text-sm">Tổng: <strong>{{ (selected?.likesPerItem || 0) * quantity }} like</strong>. Giá và chiết khấu được tính theo tài khoản khi thanh toán; admin được miễn phí theo chính sách shop.</p>
      <div v-if="selected" class="rounded-xl border border-orange-200 bg-orange-50 p-4 space-y-2 text-sm" aria-live="polite">
        <div class="flex justify-between"><span>Giá niêm yết / gói</span><strong>{{ formatVND(selected.price) }}</strong></div>
        <div class="flex justify-between"><span>Thành tiền ({{ safeQuantity }} gói)</span><strong>{{ formatVND(subtotal) }}</strong></div>
        <div v-if="auth.isAdmin" class="flex justify-between text-emerald-700"><span>Ưu đãi admin — giảm 100%</span><strong>−{{ formatVND(subtotal) }}</strong></div>
        <div v-else-if="auth.userTierDiscount > 0" class="flex justify-between text-emerald-700"><span>Chiết khấu cấp bậc {{ auth.userTierDiscount }}%</span><strong>−{{ formatVND(subtotal - estimatedTotal) }}</strong></div>
        <div class="flex justify-between border-t border-orange-200 pt-2 text-base font-bold text-orange-700"><span>{{ auth.isAdmin ? 'Cần thanh toán' : 'Thanh toán dự kiến' }}</span><span>{{ formatVND(estimatedTotal) }}</span></div>
        <p v-if="auth.isAdmin" class="text-xs text-stone-600">Đơn admin miễn phí, không trừ tiền ví.</p>
        <p v-else class="text-xs text-stone-600">Dự kiến theo giá gói và chiết khấu cấp bậc. Nếu tài khoản có giá riêng cho sản phẩm, backend áp dụng giá riêng khi tạo đơn.</p>
      </div>
      <button :disabled="busy || !selected" class="bg-orange-600 text-white rounded-lg px-5 py-2 disabled:opacity-50">{{ busy ? 'Đang quét bài và kiểm tra đơn...' : 'Đặt đơn buff like' }}</button>
      <p v-if="busy" role="status" class="text-sm text-orange-700">Đang tìm nhân vật và kiểm tra bài đăng. Vui lòng chờ kết quả.</p>
      <div v-if="message" :role="messageIsError ? 'alert' : 'status'" class="rounded-xl border p-4 text-sm" :class="messageIsError ? 'border-rose-300 bg-rose-50 text-rose-800' : 'border-emerald-200 bg-emerald-50 text-emerald-800'">
        <p class="font-bold mb-1">{{ messageIsError ? 'Không thể đặt đơn' : 'Đặt đơn thành công' }}</p>
        <p>{{ message }}</p>
      </div>
    </form>
    <div class="bg-white border rounded-2xl p-5 space-y-3">
      <div class="flex justify-between"><h2 class="font-bold">{{ auth.isAdmin ? 'Hàng đợi PC (tất cả khách)' : 'Đơn buff like của bạn' }}</h2><button @click="loadJobs" class="text-orange-600 text-sm">Làm mới</button></div>
      <p v-if="jobsError" class="text-rose-600 text-sm">{{ jobsError }}</p>
      <p v-if="!jobs.length" class="text-sm text-stone-500">Chưa có đơn.</p>
      <div v-for="job in jobs" :key="job.order_id" class="border-t pt-3 text-sm space-y-1">
        <div class="font-semibold">{{ job.order_code }} — {{ job.target_name }}</div>
        <div>{{ labels[job.state] || job.state }} · {{ job.done }} / {{ job.requested }} like</div>
        <progress :value="job.done" :max="job.requested" class="w-full"></progress>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { apiClient } from '@/services/api'
import { productService } from '@/services/product.service'
import { useAuthStore } from '@/stores/auth'
import { formatVND } from '@/utils/format'
import type { Product } from '@/types'
const auth = useAuthStore()
const products = ref<Product[]>([])
const productId = ref('')
const targetName = ref('')
const quantity = ref(1)
const selected = computed(() => products.value.find(p => p.id === productId.value))
const safeQuantity = computed(() => Number.isInteger(quantity.value) && quantity.value > 0 ? quantity.value : 0)
const subtotal = computed(() => (selected.value?.price || 0) * safeQuantity.value)
const estimatedTotal = computed(() => {
  if (auth.isAdmin) return 0
  const unitPrice = Math.max(0, Math.round((selected.value?.price || 0) * (100 - auth.userTierDiscount) / 100))
  return unitPrice * safeQuantity.value
})
const busy = ref(false)
const message = ref('')
const messageIsError = ref(false)
const jobsError = ref('')
const jobs = ref<Array<{order_id: string; order_code: string; target_name: string; requested: number; done: number; state: string}>>([])
const labels: Record<string, string> = {queued: 'Chờ PC nhận', claimed: 'PC đã nhận', running: 'Đang chạy', completed: 'Hoàn thành', needs_review: 'Cần kiểm tra engine'}
let timer: ReturnType<typeof setInterval> | undefined
let pending: { key: string; body: string } | null = null
async function loadJobs() {
  try {
    jobs.value = (await apiClient.get(auth.isAdmin ? '/admin/buff-like/jobs' : '/buff-like/jobs')).data
    jobsError.value = ''
  } catch { jobsError.value = 'Không tải được tiến độ. Kiểm tra kết nối backend.' }
}
async function submit() {
  if (busy.value) return
  const body = JSON.stringify({items: [{productId: productId.value, quantity: quantity.value, customerInput: {targetName: targetName.value.trim()}}]})
  if (pending && pending.body !== body) {
    messageIsError.value = true
    message.value = 'Yêu cầu trước chưa rõ kết quả. Giữ nguyên thông tin và thử lại để lấy đúng đơn, hoặc kiểm tra lịch sử trước.'
    return
  }
  pending ||= {key: crypto.randomUUID(), body}
  busy.value = true
  message.value = ''
  messageIsError.value = false
  try {
    const result = await apiClient.post('/orders', JSON.parse(body), {headers: {'Idempotency-Key': pending.key}})
    pending = null
    const paid = Number(result.data.total_amount ?? result.data.totalAmount)
    message.value = `Đã xếp hàng đơn ${result.data.order_code || result.data.orderCode}.${Number.isFinite(paid) ? ` Thanh toán thực tế: ${formatVND(paid)}.` : ''}`
    await loadJobs()
  } catch (err: any) {
    const errorCode = err.response?.data?.error?.code
    // These scanner errors explicitly guarantee checkout has not created an order.
    if ((err.response?.status >= 400 && err.response.status < 500) || errorCode === 'SCAN_UNAVAILABLE') pending = null
    messageIsError.value = true
    message.value = err.response?.data?.error?.message || 'Chưa xác nhận tạo đơn. Thử lại cùng thông tin để tránh trùng đơn.'
  } finally { busy.value = false }
}
onMounted(async () => {
  try { products.value = (await productService.getProducts()).filter(p => p.productType === 'buff_like') }
  catch { messageIsError.value = true; message.value = 'Không tải được gói dịch vụ.' }
  await loadJobs()
  timer = setInterval(loadJobs, 5000)
})
onUnmounted(() => { if (timer) clearInterval(timer) })
</script>
