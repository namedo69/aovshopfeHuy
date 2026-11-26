<template>
  <div class="min-h-screen flex flex-col bg-[#fafaf9] text-stone-800 antialiased selection:bg-amber-200 selection:text-amber-900">
    <!-- Top Announcement Bar -->
    <div class="bg-gradient-to-r from-amber-500 via-orange-500 to-amber-600 text-white text-xs py-1.5 px-4 font-medium shadow-xs">
      <div class="max-w-7xl mx-auto flex items-center justify-between">
        <div class="flex items-center gap-2">
          <span class="inline-flex items-center gap-1.5 bg-black/15 backdrop-blur-xs px-2.5 py-0.5 rounded-full text-[11px] font-bold tracking-wide uppercase">
            <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-pulse"></span>
            Hệ thống 24/7
          </span>
          <span class="hidden sm:inline text-amber-100/90 text-xs">Nạp tiền VietQR tự động gạch sau 3 giây • Điều phối đa luồng bảo đảm 100%</span>
        </div>
        <div class="flex items-center gap-4 text-xs">
          <a href="https://zalo.me/0906772683" target="_blank" rel="noopener noreferrer" class="hover:text-amber-100 flex items-center gap-1 font-semibold transition">
            <Phone class="w-3 h-3" /> 0906772683
          </a>
          <span v-if="appEnv !== 'production'" class="bg-black/25 px-2 py-0.5 rounded text-[10px] font-bold uppercase tracking-wider">
            {{ appEnv }}
          </span>
        </div>
      </div>
    </div>

    <!-- Floating Glass Header -->
    <header class="sticky top-0 z-40 bg-white/90 backdrop-blur-xl border-b border-amber-100/80 shadow-xs transition-all">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-4">
        <!-- Logo -->
        <router-link to="/" class="flex items-center gap-2.5 group shrink-0">
          <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-amber-500 via-orange-500 to-amber-400 flex items-center justify-center text-white shadow-md shadow-orange-500/25 group-hover:scale-105 group-hover:rotate-3 transition-all duration-300">
            <Sparkles class="w-5 h-5 drop-shadow-xs" />
          </div>
          <div class="flex flex-col">
            <span class="text-xl font-extrabold bg-gradient-to-r from-amber-600 via-orange-600 to-amber-500 bg-clip-text text-transparent tracking-tight">
              chaysk<span class="text-amber-600">.com</span>
            </span>
            <span class="text-[10px] font-semibold text-stone-400 tracking-wider -mt-1 uppercase">Dịch vụ game tự động</span>
          </div>
        </router-link>

        <!-- Navigation Links (Centered Desktop) -->
        <nav class="hidden lg:flex items-center gap-1 bg-stone-100/80 p-1 rounded-2xl border border-stone-200/60 shadow-inner">
          <router-link to="/buff-like" class="px-3.5 py-1.5 rounded-xl text-orange-700 text-xs font-semibold hover:bg-white">♥ Buff Like</router-link>
          <router-link
            to="/products"
            class="px-3.5 py-1.5 rounded-xl text-stone-600 hover:text-stone-900 hover:bg-white text-xs font-semibold transition-all"
            active-class="bg-white text-orange-600 shadow-xs font-bold"
          >
            ⚡ Gói dịch vụ
          </router-link>
          <router-link
            to="/group-chest"
            class="px-3.5 py-1.5 rounded-xl text-stone-600 hover:text-stone-900 hover:bg-white text-xs font-semibold transition-all flex items-center gap-1.5"
            active-class="bg-white text-orange-600 shadow-xs font-bold"
          >
            <span>🐉 Mở rương</span>
            <span class="px-1.5 py-0.2 bg-amber-500/15 text-amber-700 text-[10px] font-bold rounded-md">HOT</span>
          </router-link>
          <router-link
            v-if="authStore.isAuthenticated"
            to="/orders"
            class="px-3.5 py-1.5 rounded-xl text-stone-600 hover:text-stone-900 hover:bg-white text-xs font-semibold transition-all"
            active-class="bg-white text-orange-600 shadow-xs font-bold"
          >
            📦 Lịch sử đơn
          </router-link>
          <a
            href="https://zalo.me/0906772683"
            target="_blank"
            rel="noopener noreferrer"
            class="px-3.5 py-1.5 rounded-xl text-amber-700 hover:text-amber-900 hover:bg-amber-50/80 text-xs font-semibold transition-all flex items-center gap-1"
          >
            <MessageCircle class="w-3.5 h-3.5 text-amber-600" />
            <span>Hỗ trợ Zalo</span>
          </a>
        </nav>

        <!-- Right Side / User Actions -->
        <div class="flex items-center gap-2.5">
          <template v-if="authStore.isAuthenticated">
            <!-- Balance pill -->
            <router-link
              to="/wallet"
              class="flex items-center gap-2 bg-gradient-to-r from-amber-50 to-orange-50 hover:from-amber-100 hover:to-orange-100 border border-amber-200/80 text-amber-900 px-3.5 py-1.5 rounded-full text-xs font-bold transition-all shadow-xs"
            >
              <Wallet class="w-4 h-4 text-orange-600 shrink-0" />
              <span>{{ formatVND(authStore.userBalance) }}</span>
            </router-link>

            <!-- Quick deposit button -->
            <router-link
              to="/deposit"
              class="hidden sm:inline-flex items-center gap-1.5 bg-gradient-to-r from-amber-500 to-orange-600 hover:from-amber-600 hover:to-orange-700 text-white px-4 py-1.5 rounded-full text-xs font-bold shadow-sm shadow-orange-500/25 transition-all hover:shadow-md hover:scale-[1.02]"
            >
              <PlusCircle class="w-3.5 h-3.5" />
              <span>Nạp ví</span>
            </router-link>

            <!-- User Menu Trigger -->
            <div class="relative" ref="userMenuRef">
              <button
                @click="isUserMenuOpen = !isUserMenuOpen"
                class="flex items-center gap-2 text-stone-700 p-0.5 rounded-full hover:ring-2 hover:ring-amber-400/50 transition cursor-pointer"
              >
                <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-amber-500 to-orange-500 text-white font-black text-xs flex items-center justify-center shadow-xs">
                  {{ userInitial }}
                </div>
              </button>
              <!-- Dropdown menu -->
              <div
                v-show="isUserMenuOpen"
                class="absolute right-0 mt-2 w-60 bg-white rounded-2xl shadow-xl border border-stone-200/80 py-2 z-50 animate-in fade-in zoom-in-95 duration-150"
              >
                <div class="px-4 py-2.5 border-b border-stone-100 text-xs">
                  <span class="text-stone-400 block text-[11px]">Đang đăng nhập:</span>
                  <strong class="text-stone-800 block truncate font-semibold text-xs mt-0.5">{{ authStore.user?.email }}</strong>
                </div>
                <div class="p-1 space-y-0.5">
                  <router-link
                    to="/wallet"
                    @click="isUserMenuOpen = false"
                    class="flex items-center justify-between px-3 py-2 text-xs font-medium text-stone-700 rounded-xl hover:bg-amber-50 hover:text-orange-700 transition"
                  >
                    <span class="flex items-center gap-2"><Wallet class="w-4 h-4 text-orange-500" /> Quản lý số dư</span>
                    <span class="font-bold text-orange-600">{{ formatVND(authStore.userBalance) }}</span>
                  </router-link>
                  <router-link
                    to="/orders"
                    @click="isUserMenuOpen = false"
                    class="flex items-center gap-2 px-3 py-2 text-xs font-medium text-stone-700 rounded-xl hover:bg-amber-50 hover:text-orange-700 transition"
                  >
                    <Package class="w-4 h-4 text-orange-500" /> Đơn hàng của tôi
                  </router-link>
                  <a
                    href="https://zalo.me/0906772683"
                    target="_blank"
                    rel="noopener noreferrer"
                    @click="isUserMenuOpen = false"
                    class="flex items-center gap-2 px-3 py-2 text-xs font-medium text-amber-700 rounded-xl hover:bg-amber-50 transition"
                  >
                    <MessageCircle class="w-4 h-4 text-amber-600" /> Liên hệ Zalo
                  </a>
                  <router-link
                    v-if="authStore.isAdmin"
                    to="/admin"
                    @click="isUserMenuOpen = false"
                    class="flex items-center gap-2 px-3 py-2 text-xs font-bold text-orange-700 rounded-xl bg-orange-50/70 hover:bg-orange-100/70 transition"
                  >
                    <ShieldCheck class="w-4 h-4 text-orange-600" /> Quản trị Admin
                  </router-link>
                </div>
                <div class="my-1 border-t border-stone-100"></div>
                <div class="p-1">
                  <button
                    @click="handleLogout"
                    class="w-full text-left flex items-center gap-2 px-3 py-2 text-xs font-medium text-rose-600 rounded-xl hover:bg-rose-50 transition cursor-pointer"
                  >
                    <LogOut class="w-4 h-4" /> Đăng xuất
                  </button>
                </div>
              </div>
            </div>
          </template>

          <template v-else>
            <router-link
              to="/login"
              class="text-stone-600 hover:text-orange-600 font-semibold text-xs px-3 py-2 rounded-xl hover:bg-stone-100 transition"
            >
              Đăng nhập
            </router-link>
            <router-link
              to="/register"
              class="bg-gradient-to-r from-amber-500 to-orange-600 hover:from-amber-600 hover:to-orange-700 text-white text-xs font-bold px-4 py-2 rounded-xl shadow-xs shadow-orange-500/25 transition hover:shadow-md hover:scale-[1.02]"
            >
              Đăng ký ngay
            </router-link>
          </template>

          <!-- Mobile Hamburger Toggle -->
          <button
            @click="isMobileMenuOpen = !isMobileMenuOpen"
            class="lg:hidden p-2 text-stone-600 hover:text-stone-900 rounded-xl hover:bg-stone-100 transition cursor-pointer"
            aria-label="Menu"
          >
            <component :is="isMobileMenuOpen ? X : Menu" class="w-5 h-5" />
          </button>
        </div>
      </div>

      <!-- Mobile Navigation Drawer -->
      <div v-show="isMobileMenuOpen" class="lg:hidden border-t border-amber-100 bg-white/95 backdrop-blur-xl px-4 py-3 space-y-2 animate-in slide-in-from-top-2 duration-150">
        <router-link to="/buff-like" @click="isMobileMenuOpen = false" class="block px-3 py-2 rounded-xl text-xs font-bold text-orange-700">♥ Buff Like</router-link>
        <router-link
          to="/products"
          @click="isMobileMenuOpen = false"
          class="flex items-center gap-2 px-3 py-2 rounded-xl text-xs font-bold text-stone-700 hover:bg-amber-50 hover:text-orange-600 transition"
        >
          ⚡ Gói dịch vụ
        </router-link>
        <router-link
          to="/group-chest"
          @click="isMobileMenuOpen = false"
          class="flex items-center justify-between px-3 py-2 rounded-xl text-xs font-bold text-stone-700 hover:bg-amber-50 hover:text-orange-600 transition"
        >
          <span class="flex items-center gap-2">🐉 Mở rương nhóm</span>
          <span class="px-1.5 py-0.2 bg-amber-500/20 text-amber-800 text-[10px] font-bold rounded">HOT</span>
        </router-link>
        <router-link
          to="/deposit"
          @click="isMobileMenuOpen = false"
          class="flex items-center gap-2 px-3 py-2 rounded-xl text-xs font-bold text-orange-700 bg-amber-50/80 transition"
        >
          💳 Nạp tiền VietQR tự động
        </router-link>
        <router-link
          v-if="authStore.isAuthenticated"
          to="/orders"
          @click="isMobileMenuOpen = false"
          class="flex items-center gap-2 px-3 py-2 rounded-xl text-xs font-bold text-stone-700 hover:bg-amber-50 hover:text-orange-600 transition"
        >
          📦 Lịch sử đơn hàng
        </router-link>
        <a
          href="https://zalo.me/0906772683"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 px-3 py-2 rounded-xl text-xs font-bold text-amber-700 hover:bg-amber-50 transition"
        >
          <MessageCircle class="w-4 h-4 text-amber-600" /> Zalo Hỗ Trợ Khách Hàng
        </a>
      </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-1">
      <router-view />
    </main>

    <!-- Distinctive Modern Footer -->
    <footer class="bg-stone-900 text-stone-400 mt-16 pt-14 pb-8 border-t border-stone-800 text-xs">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-10 pb-12 border-b border-stone-800">
          <!-- Col 1: Brand & Bio -->
          <div class="md:col-span-2 space-y-4">
            <div class="flex items-center gap-2.5">
              <div class="w-9 h-9 rounded-xl bg-gradient-to-tr from-amber-500 to-orange-500 flex items-center justify-center text-white shadow-md shadow-orange-500/20">
                <Sparkles class="w-4 h-4" />
              </div>
              <span class="text-xl font-black text-white tracking-tight">chaysk<span class="text-amber-500">.com</span></span>
            </div>
            <p class="text-stone-400 max-w-md leading-relaxed text-xs">
              Nền tảng cung cấp dịch vụ và tài khoản game Liên Quân tự động 100%. Nạp tiền thông minh qua VietQR gạch thẻ tự động không cần người duyệt, đảm bảo tốc độ và bảo mật tối đa.
            </p>
            <div class="pt-2 flex flex-wrap gap-4 text-stone-300">
              <a href="https://zalo.me/0906772683" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-2 bg-stone-800/80 hover:bg-stone-800 border border-stone-700/60 px-3.5 py-2 rounded-xl text-xs transition">
                <Phone class="w-3.5 h-3.5 text-amber-500" />
                <span>Zalo Admin: <strong class="text-white">0906772683</strong></span>
              </a>
              <a href="https://www.facebook.com/share/1DdtvRv99p/" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-2 bg-amber-500/10 hover:bg-amber-500/20 border border-amber-500/30 text-amber-400 px-3.5 py-2 rounded-xl text-xs transition font-semibold">
                <Users class="w-3.5 h-3.5" />
                <span>Liên hệ Facebook</span>
              </a>
            </div>
          </div>

          <!-- Col 2: Services -->
          <div>
            <h4 class="text-stone-200 font-bold uppercase tracking-wider text-[11px] mb-4">Dịch vụ</h4>
            <ul class="space-y-2.5">
              <li><router-link to="/products" class="hover:text-amber-400 transition">Danh sách gói dịch vụ</router-link></li>
              <li><router-link to="/group-chest" class="hover:text-amber-400 transition">Mở rương code chung sức</router-link></li>
              <li><router-link to="/deposit" class="hover:text-amber-400 transition">Nạp tiền VietQR tự động</router-link></li>
              <li><router-link to="/orders" class="hover:text-amber-400 transition">Tra cứu trạng thái đơn</router-link></li>
            </ul>
          </div>

          <!-- Col 3: Support -->
          <div>
            <h4 class="text-stone-200 font-bold uppercase tracking-wider text-[11px] mb-4">Hỗ trợ 24/7</h4>
            <ul class="space-y-2.5">
              <li>
                <a href="https://www.facebook.com/share/1DdtvRv99p/" target="_blank" rel="noopener noreferrer" class="hover:text-amber-400 inline-flex items-center gap-1.5 transition">
                  <MessageCircle class="w-3.5 h-3.5 text-amber-500" />
                  <span>Facebook hỗ trợ</span>
                </a>
              </li>
              <li>
                <a href="https://zalo.me/0906772683" target="_blank" rel="noopener noreferrer" class="hover:text-amber-400 inline-flex items-center gap-1.5 transition">
                  <Phone class="w-3.5 h-3.5 text-emerald-400" />
                  <span>Zalo: 0906772683</span>
                </a>
              </li>
              <li>
                <a href="mailto:huynhlegiahuy93@gmail.com" class="hover:text-amber-400 break-all transition">
                  huynhlegiahuy93@gmail.com
                </a>
              </li>
              <li class="pt-2 text-stone-500 text-[11px]">
                Thời gian giải đáp: 24/7 cả ngày lễ & cuối tuần.
              </li>
            </ul>
          </div>
        </div>

        <div class="mt-8 flex flex-col sm:flex-row justify-between items-center text-[11px] text-stone-500 gap-4">
          <span>© 2026 chaysk.com • Vận hành bởi hệ thống điều phối đa luồng.</span>
          <div class="flex items-center gap-3">
            <span class="inline-flex items-center gap-1.5 bg-emerald-950/60 text-emerald-400 border border-emerald-800/40 px-2.5 py-1 rounded-full text-[10px] font-semibold">
              <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-ping"></span>
              All Services Operational
            </span>
          </div>
        </div>
      </div>
    </footer>

    <!-- Floating Zalo Button -->
    <a
      href="https://zalo.me/0906772683"
      target="_blank"
      rel="noopener noreferrer"
      title="Liên hệ Zalo 0906772683"
      class="fixed bottom-6 right-6 z-50 flex items-center gap-2.5 bg-gradient-to-r from-amber-500 to-orange-600 hover:from-amber-600 hover:to-orange-700 text-white px-4 py-2.5 rounded-full shadow-lg shadow-orange-600/30 hover:shadow-xl hover:scale-105 transition-all group cursor-pointer"
    >
      <div class="w-7 h-7 rounded-full bg-white text-orange-600 flex items-center justify-center font-bold shadow-xs group-hover:rotate-12 transition-transform">
        <MessageCircle class="w-4 h-4 fill-orange-600" />
      </div>
      <div class="text-left hidden sm:block pr-1">
        <div class="text-[10px] text-amber-100 font-medium leading-none">Hỗ trợ 24/7</div>
        <div class="text-xs font-bold leading-tight">Chat Zalo ngay</div>
      </div>
    </a>
  </div>
</template>

<script setup lang="ts">
import { computed, ref, onMounted, onUnmounted } from 'vue'
import { useRouter } from 'vue-router'
import { useAuthStore } from '@/stores/auth'
import { formatVND } from '@/utils/format'
import {
  Sparkles,
  Wallet,
  PlusCircle,
  ShieldCheck,
  Package,
  LogOut,
  MessageCircle,
  Phone,
  Users,
  Menu,
  X,
} from 'lucide-vue-next'

const authStore = useAuthStore()
const router = useRouter()

const isUserMenuOpen = ref(false)
const isMobileMenuOpen = ref(false)
const userMenuRef = ref<HTMLElement | null>(null)

const appEnv = import.meta.env.VITE_APP_ENV || 'production'

const userInitial = computed(() => {
  if (!authStore.user?.email) return 'U'
  return authStore.user.email.charAt(0).toUpperCase()
})

const handleClickOutside = (event: MouseEvent) => {
  if (userMenuRef.value && !userMenuRef.value.contains(event.target as Node)) {
    isUserMenuOpen.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside)
})

const handleLogout = async () => {
  isUserMenuOpen.value = false
  await authStore.logout()
  router.push('/login')
}
</script>
