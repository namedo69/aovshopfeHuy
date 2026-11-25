<template>
  <div class="space-y-12">
    <!-- Asymmetric Modern Hero Section -->
    <section class="relative overflow-hidden bg-gradient-to-b from-amber-50/70 via-orange-50/30 to-[#fafaf9] pt-10 pb-16 border-b border-amber-100/60">
      <!-- Ambient decorative glow orbs -->
      <div class="absolute -top-32 -left-32 w-96 h-96 rounded-full bg-amber-300/25 blur-3xl pointer-events-none"></div>
      <div class="absolute top-20 -right-20 w-96 h-96 rounded-full bg-orange-300/20 blur-3xl pointer-events-none"></div>

      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">

          <!-- Left Column: Impact Content & CTAs (7 cols) -->
          <div class="lg:col-span-7 space-y-6 text-left">
            <!-- Badge -->
            <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full text-xs font-bold bg-white border border-amber-200 shadow-xs text-amber-900">
              <span class="flex h-2 w-2 relative">
                <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-orange-400 opacity-75"></span>
                <span class="relative inline-flex rounded-full h-2 w-2 bg-orange-500"></span>
              </span>
              <span>Hệ thống tự động hóa thế hệ mới • 100% Không cần đợi duyệt</span>
            </div>

            <!-- Headline -->
            <h1 class="text-4xl sm:text-5xl lg:text-6xl font-black text-stone-900 tracking-tight leading-[1.15]">
              Dịch Vụ Game <br />
              <span class="bg-gradient-to-r from-amber-500 via-orange-500 to-amber-600 bg-clip-text text-transparent">
                Xử Lý Siêu Tốc
              </span>
              <span class="text-stone-800"> 3 Giây</span>
            </h1>

            <!-- Description -->
            <p class="text-base sm:text-lg text-stone-600 max-w-xl leading-relaxed">
              Tự động hóa hoàn toàn từ nạp ví VietQR, áp mã voucher cấp bậc, đến gạch đơn tức thì qua hệ thống WebSocket điều phối đa luồng.
            </p>

            <!-- Action Buttons -->
            <div class="pt-2 flex flex-wrap items-center gap-3.5">
              <router-link
                to="/products"
                class="px-6 py-3.5 rounded-2xl bg-gradient-to-r from-amber-500 via-orange-500 to-orange-600 hover:from-amber-600 hover:to-orange-700 text-white font-bold text-sm shadow-md shadow-orange-500/25 transition-all hover:shadow-lg hover:-translate-y-0.5 flex items-center gap-2"
              >
                <Zap class="w-4 h-4 fill-current" />
                <span>Khám phá các gói</span>
              </router-link>

              <router-link
                to="/group-chest"
                class="px-5 py-3.5 rounded-2xl bg-white hover:bg-amber-50/60 text-stone-800 font-bold text-sm border border-amber-200/80 shadow-xs transition-all hover:border-orange-400 hover:-translate-y-0.5 flex items-center gap-2"
              >
                <span>🐉 Mở rương may mắn</span>
                <span class="px-1.5 py-0.5 rounded bg-orange-500 text-white text-[10px] font-black uppercase">Mới</span>
              </router-link>

              <router-link
                to="/deposit"
                class="px-4 py-3.5 text-orange-700 hover:text-orange-800 font-semibold text-xs flex items-center gap-1.5 hover:underline"
              >
                <QrCode class="w-4 h-4" />
                <span>Nạp ví VietQR</span>
              </router-link>
            </div>

            <!-- Trust Metrics Ribbon -->
            <div class="pt-6 grid grid-cols-3 gap-4 border-t border-amber-100 max-w-lg">
              <div>
                <div class="text-2xl font-black text-stone-900 tracking-tight">~ 3s</div>
                <div class="text-[11px] text-stone-500 font-medium">Thời gian gạch thẻ</div>
              </div>
              <div class="border-l border-amber-100 pl-4">
                <div class="text-2xl font-black text-orange-600 tracking-tight">100%</div>
                <div class="text-[11px] text-stone-500 font-medium">Tự động VietQR</div>
              </div>
              <div class="border-l border-amber-100 pl-4">
                <div class="text-2xl font-black text-amber-600 tracking-tight">24/7</div>
                <div class="text-[11px] text-stone-500 font-medium">Hỗ trợ kỹ thuật</div>
              </div>
            </div>
          </div>

          <!-- Right Column: Interactive Quick Card (5 cols) -->
          <div class="lg:col-span-5">
            <div class="bg-white/80 backdrop-blur-xl border border-amber-200/80 rounded-3xl p-6 sm:p-7 shadow-xl shadow-amber-900/5 relative overflow-hidden space-y-5">
              <!-- Header inside card -->
              <div class="flex items-center justify-between border-b border-stone-100 pb-4">
                <div class="flex items-center gap-2.5">
                  <div class="w-9 h-9 rounded-xl bg-gradient-to-tr from-amber-500 to-orange-500 flex items-center justify-center text-white shadow-xs">
                    <QrCode class="w-5 h-5" />
                  </div>
                  <div>
                    <h3 class="font-bold text-stone-900 text-sm">Nạp Tiền VietQR Tự Động</h3>
                    <p class="text-[11px] text-stone-400">Quét mã chuyển khoản tức thì 24/7</p>
                  </div>
                </div>
                <span class="inline-flex items-center gap-1 text-[11px] font-bold text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded-full border border-emerald-200/60">
                  <span class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"></span> Sẵn sàng
                </span>
              </div>

              <!-- Fast Amount Selector -->
              <div class="space-y-2.5">
                <label class="text-[11px] font-bold text-stone-500 uppercase tracking-wider block">Chọn nhanh mệnh giá</label>
                <div class="grid grid-cols-2 sm:grid-cols-4 gap-2">
                  <button
                    v-for="amt in [20000, 50000, 100000, 200000]"
                    :key="amt"
                    @click="selectedQuickAmount = amt"
                    :class="[
                      'py-2 px-2 rounded-xl text-xs font-bold border transition text-center cursor-pointer',
                      selectedQuickAmount === amt
                        ? 'border-orange-500 bg-orange-50 text-orange-700 shadow-xs'
                        : 'border-stone-200 bg-stone-50/60 text-stone-700 hover:bg-stone-100'
                    ]"
                  >
                    {{ formatVND(amt) }}
                  </button>
                </div>
              </div>

              <!-- Quick CTA Box -->
              <div class="bg-gradient-to-r from-amber-50 to-orange-50 rounded-2xl p-4 border border-amber-200/60 space-y-3">
                <div class="flex items-center justify-between text-xs">
                  <span class="text-stone-600 font-medium">Số tiền muốn nạp:</span>
                  <span class="text-base font-extrabold text-orange-600">{{ formatVND(selectedQuickAmount) }}</span>
                </div>
                <router-link
                  :to="{ path: '/deposit', query: { amount: selectedQuickAmount } }"
                  class="w-full py-2.5 px-4 rounded-xl bg-gradient-to-r from-amber-500 to-orange-600 hover:from-amber-600 hover:to-orange-700 text-white font-bold text-xs flex items-center justify-center gap-2 shadow-sm transition hover:shadow cursor-pointer"
                >
                  <Sparkles class="w-4 h-4" />
                  <span>Tạo mã QR Nạp Ngay</span>
                </router-link>
              </div>

              <!-- Real-time Status ticker -->
              <div class="pt-1 flex items-center justify-between text-[11px] text-stone-500">
                <span class="flex items-center gap-1.5">
                  <ShieldCheck class="w-3.5 h-3.5 text-emerald-600" />
                  <span>Xác thực HMAC-SHA256</span>
                </span>
                <span class="text-orange-600 font-semibold">Cộng tiền trong 3s</span>
              </div>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- Distinctive Feature / Value Pillars Grid -->
    <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- Feature 1 -->
        <div class="relative p-6 rounded-3xl bg-white border border-amber-100 shadow-xs hover:shadow-lg hover:border-amber-300 transition-all group overflow-hidden">
          <div class="absolute top-0 left-0 right-0 h-1 bg-gradient-to-r from-amber-400 to-orange-500 opacity-0 group-hover:opacity-100 transition-opacity"></div>
          <div class="w-12 h-12 rounded-2xl bg-amber-50 text-orange-600 flex items-center justify-center mb-4 group-hover:scale-110 group-hover:bg-orange-50 transition-all">
            <Zap class="w-6 h-6 fill-current" />
          </div>
          <h3 class="text-base font-extrabold text-stone-900 group-hover:text-orange-600 transition-colors">Điều Phối Đa Luồng</h3>
          <p class="mt-2 text-stone-600 text-xs leading-relaxed">
            Hệ thống tự động phân luồng công việc qua WebSocket worker phân tán, đảm bảo không nghẽn lệnh vào giờ cao điểm.
          </p>
        </div>

        <!-- Feature 2 -->
        <div class="relative p-6 rounded-3xl bg-white border border-amber-100 shadow-xs hover:shadow-lg hover:border-amber-300 transition-all group overflow-hidden">
          <div class="absolute top-0 left-0 right-0 h-1 bg-gradient-to-r from-amber-400 to-orange-500 opacity-0 group-hover:opacity-100 transition-opacity"></div>
          <div class="w-12 h-12 rounded-2xl bg-amber-50 text-orange-600 flex items-center justify-center mb-4 group-hover:scale-110 group-hover:bg-orange-50 transition-all">
            <QrCode class="w-6 h-6" />
          </div>
          <h3 class="text-base font-extrabold text-stone-900 group-hover:text-orange-600 transition-colors">Quét VietQR Tức Thì</h3>
          <p class="mt-2 text-stone-600 text-xs leading-relaxed">
            Mã QR tự sinh có nội dung chuyển khoản mã hóa, hệ thống SePay tự động gạch và cộng tiền vào ví trong 3 giây.
          </p>
        </div>

        <!-- Feature 3 -->
        <div class="relative p-6 rounded-3xl bg-white border border-amber-100 shadow-xs hover:shadow-lg hover:border-amber-300 transition-all group overflow-hidden">
          <div class="absolute top-0 left-0 right-0 h-1 bg-gradient-to-r from-amber-400 to-orange-500 opacity-0 group-hover:opacity-100 transition-opacity"></div>
          <div class="w-12 h-12 rounded-2xl bg-amber-50 text-orange-600 flex items-center justify-center mb-4 group-hover:scale-110 group-hover:bg-orange-50 transition-all">
            <ShieldCheck class="w-6 h-6" />
          </div>
          <h3 class="text-base font-extrabold text-stone-900 group-hover:text-orange-600 transition-colors">Cấp Bậc & Chiết Khấu</h3>
          <p class="mt-2 text-stone-600 text-xs leading-relaxed">
            Hỗ trợ phân cấp thành viên (User Tiers) tự động áp dụng giá ưu đãi đại lý độc quyền trên từng mã đơn hàng.
          </p>
        </div>
      </div>
    </section>

    <!-- Featured Products Preview with Modern Layout -->
    <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
      <div class="flex flex-col sm:flex-row sm:items-end justify-between mb-8 gap-4 border-b border-stone-200/80 pb-5">
        <div>
          <div class="inline-flex items-center gap-1.5 text-xs font-bold text-orange-600 uppercase tracking-wider mb-1">
            <Sparkles class="w-3.5 h-3.5" /> Bảng giá cập nhật mới nhất
          </div>
          <h2 class="text-2xl sm:text-3xl font-black text-stone-900 tracking-tight">Gói Dịch Vụ Nổi Bật</h2>
        </div>

        <div class="flex items-center gap-3">
          <router-link
            to="/group-chest"
            class="px-4 py-2 rounded-xl text-xs font-bold bg-amber-100/70 hover:bg-amber-100 text-amber-900 transition flex items-center gap-1.5"
          >
            <span>🐉 Mở rương nhóm</span>
          </router-link>
          <router-link
            to="/products"
            class="px-4 py-2 rounded-xl text-xs font-bold bg-stone-900 hover:bg-stone-800 text-white transition flex items-center gap-1.5 shadow-xs"
          >
            <span>Xem tất cả gói</span>
            <ArrowRight class="w-3.5 h-3.5" />
          </router-link>
        </div>
      </div>

      <!-- Loading skeleton -->
      <div v-if="isLoading" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="n in 3" :key="n" class="rounded-3xl bg-white border border-stone-200 p-6 animate-pulse space-y-4">
          <div class="h-4 bg-stone-200 rounded w-20"></div>
          <div class="h-6 bg-stone-200 rounded w-3/4"></div>
          <div class="h-12 bg-stone-100 rounded w-full"></div>
          <div class="h-8 bg-stone-200 rounded w-1/2"></div>
        </div>
      </div>

      <!-- Product Cards Grid -->
      <div v-else-if="featuredProducts.length > 0" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div
          v-for="item in featuredProducts"
          :key="item.id"
          class="rounded-3xl bg-white border border-stone-200/90 hover:border-orange-400/80 hover:shadow-xl hover:shadow-orange-500/10 transition-all duration-300 flex flex-col overflow-hidden group"
        >
          <div class="p-6 flex-1 flex flex-col justify-between space-y-4">
            <div>
              <div class="flex items-center justify-between mb-3">
                <span class="text-[11px] font-bold px-3 py-1 rounded-full bg-amber-50 text-amber-800 border border-amber-200/80">
                  {{ item.category || 'Dịch vụ Hot' }}
                </span>
                <span class="inline-flex items-center gap-1 text-[11px] font-medium text-emerald-600 bg-emerald-50 px-2 py-0.5 rounded-full">
                  <span class="w-1.5 h-1.5 rounded-full bg-emerald-500"></span> Đang sẵn hàng
                </span>
              </div>

              <h3 class="text-base sm:text-lg font-black text-stone-900 group-hover:text-orange-600 transition-colors line-clamp-1">
                {{ item.name }}
              </h3>
              <p class="mt-2 text-xs text-stone-500 leading-relaxed line-clamp-2">
                {{ item.description || 'Gói dịch vụ kích hoạt tự động qua hệ thống.' }}
              </p>
            </div>

            <div class="pt-4 border-t border-stone-100 flex items-center justify-between">
              <div>
                <span class="text-[11px] text-stone-400 block line-through" v-if="item.originalPrice > item.price">
                  {{ formatVND(item.originalPrice) }}
                </span>
                <span class="text-xl font-black text-orange-600 tracking-tight">{{ formatVND(item.price) }}</span>
              </div>
              <router-link
                :to="`/products/${item.slug}`"
                class="px-4 py-2.5 rounded-xl bg-gradient-to-r from-amber-500 to-orange-600 hover:from-amber-600 hover:to-orange-700 text-white text-xs font-bold shadow-xs shadow-orange-500/20 transition-all group-hover:shadow-md group-hover:scale-105 flex items-center gap-1.5"
              >
                <span>Đặt ngay</span>
                <ArrowRight class="w-3.5 h-3.5" />
              </router-link>
            </div>
          </div>
        </div>
      </div>

      <div v-else class="text-center py-16 bg-white rounded-3xl border border-dashed border-stone-300 text-stone-400 text-xs">
        Hiện chưa có gói dịch vụ nào sẵn sàng trong kho.
      </div>
    </section>

    <!-- Community VIP Banner -->
    <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pb-8">
      <div class="rounded-3xl bg-gradient-to-r from-stone-900 via-stone-800 to-stone-900 text-white p-8 sm:p-10 relative overflow-hidden shadow-xl">
        <div class="absolute -right-10 -bottom-10 w-64 h-64 bg-orange-500/20 rounded-full blur-3xl pointer-events-none"></div>
        <div class="relative z-10 max-w-2xl space-y-4">
          <span class="px-3 py-1 rounded-full text-[11px] font-black uppercase tracking-wider bg-amber-500 text-stone-950">
            Cộng Đồng Game Thủ
          </span>
          <h3 class="text-2xl sm:text-3xl font-black tracking-tight">
            Kết Nối Với chaysk.com Qua Facebook & Zalo
          </h3>
          <p class="text-xs sm:text-sm text-stone-300 leading-relaxed">
            Liên hệ để được tư vấn dịch vụ, hướng dẫn nạp tiền và hỗ trợ đơn hàng qua Facebook, Zalo hoặc email.
          </p>
          <div class="pt-2 flex flex-wrap items-center gap-4">
            <a
              href="https://www.facebook.com/share/1DdtvRv99p/"
              target="_blank"
              rel="noopener noreferrer"
              class="px-6 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-stone-950 font-black text-xs shadow-lg transition-all hover:scale-105 flex items-center gap-2"
            >
              <MessageCircle class="w-4 h-4 fill-stone-950" />
              <span>Liên hệ Facebook</span>
            </a>
            <a
              href="https://zalo.me/0906772683"
              target="_blank"
              rel="noopener noreferrer"
              class="text-xs text-stone-300 hover:text-white font-semibold flex items-center gap-1.5"
            >
              <Phone class="w-4 h-4 text-emerald-400" />
              <span>Zalo: 0906772683</span>
            </a>
          </div>
          <a href="mailto:huynhlegiahuy93@gmail.com" class="inline-block text-xs text-stone-300 hover:text-white break-all transition">
            Email: huynhlegiahuy93@gmail.com
          </a>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Sparkles, Zap, QrCode, ShieldCheck, ArrowRight, MessageCircle, Phone } from 'lucide-vue-next'
import { formatVND } from '@/utils/format'
import { productService } from '@/services/product.service'
import type { Product } from '@/types'

const featuredProducts = ref<Product[]>([])
const isLoading = ref(false)
const selectedQuickAmount = ref(50000)

const loadFeaturedProducts = async () => {
  isLoading.value = true
  try {
    const list = await productService.getProducts()
    list.sort((a, b) => a.price - b.price)
    featuredProducts.value = list.slice(0, 6)
  } catch (err) {
    console.warn('Không thể kết nối BE API, dùng danh sách dự phòng:', err)
    featuredProducts.value = [
      {
        id: '1',
        name: 'CSUC Gói Cơ Bản 100K',
        slug: 'csuc-co-ban',
        category: 'Gói Cơ Bản',
        description: 'Kích hoạt ngay lập tức, hỗ trợ tài khoản thường xuyên.',
        originalPrice: 120000,
        price: 99000,
        status: 'active',
        inputSchema: [],
      },
      {
        id: '2',
        name: 'CSUC Gói Tiêu Chuẩn 300K',
        slug: 'csuc-tieu-chuan',
        category: 'Gói Phổ Biến',
        description: 'Tặng kèm ưu đãi đặc biệt cho thành viên mới nạp lần đầu.',
        originalPrice: 350000,
        price: 289000,
        status: 'active',
        inputSchema: [],
      },
      {
        id: '3',
        name: 'CSUC Gói Cao Cấp 500K',
        slug: 'csuc-cao-cap',
        category: 'Gói VIP',
        description: 'Tốc độ ưu tiên hàng đầu, bảo hành trọn đời sự kiện.',
        originalPrice: 600000,
        price: 489000,
        status: 'active',
        inputSchema: [],
      },
    ]
  } finally {
    isLoading.value = false
  }
}

onMounted(() => {
  loadFeaturedProducts()
})
</script>
