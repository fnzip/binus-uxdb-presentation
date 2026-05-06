<script setup lang="ts">
const searchQuery = ref('')

const recommendations = [
  { id: 1, name: 'Anker Nano 33W Fast Charger', price: 150000, rating: 4.9, sold: 5200, trust: 95, image: '⚡' },
  { id: 2, name: 'Samsung Silicone Case A54', price: 50000, rating: 4.8, sold: 3100, trust: 92, image: '📱' },
  { id: 3, name: 'Sony WF-1000XM5 Earbuds', price: 3200000, rating: 4.9, sold: 890, trust: 98, image: '🎧' },
  { id: 4, name: 'Baseus USB-C Cable 2m', price: 45000, rating: 4.7, sold: 12000, trust: 88, image: '🔌' }
]

const flashSale = [
  { id: 5, name: 'Xiaomi Power Bank 20000mAh', price: 180000, originalPrice: 350000, rating: 4.8, trust: 91, image: '🔋' },
  { id: 6, name: 'Logitech Mouse Wireless', price: 120000, originalPrice: 250000, rating: 4.7, trust: 93, image: '🖱️' },
  { id: 7, name: 'Keyboard Mechanical TKL', price: 280000, originalPrice: 500000, rating: 4.6, trust: 87, image: '⌨️' }
]

const quickActions = [
  { label: 'Pencarian AI', icon: 'i-lucide-sparkles', to: '/pencarian', color: 'primary' as const },
  { label: 'Flash Sale', icon: 'i-lucide-zap', to: '/pencarian', color: 'primary' as const },
  { label: 'Pesanan', icon: 'i-lucide-package', to: '/pesanan', color: 'primary' as const },
  { label: 'Profil', icon: 'i-lucide-user', to: '/profil', color: 'primary' as const }
]

function formatPrice(price: number) {
  return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', minimumFractionDigits: 0 }).format(price)
}

function goSearch() {
  navigateTo({ path: '/pencarian', query: { q: searchQuery.value } })
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <header class="sticky top-0 z-40 bg-primary px-4 py-3">
      <div class="max-w-4xl mx-auto flex items-center gap-3">
        <h1 class="text-white font-bold text-lg shrink-0">
          ShopSync
        </h1>
        <form class="flex-1" @submit.prevent="goSearch">
          <UInput
            v-model="searchQuery"
            placeholder="Cari produk dengan AI..."
            icon="i-lucide-sparkles"
            size="sm"
            class="w-full"
          />
        </form>
        <NuxtLink to="/keranjang">
          <UIcon name="i-lucide-shopping-cart" class="text-white text-xl" />
        </NuxtLink>
      </div>
    </header>

    <!-- Hero Banner -->
    <section class="bg-gradient-to-br from-orange-50 to-amber-100 dark:from-orange-950 dark:to-amber-900 px-4 py-6">
      <div class="max-w-4xl mx-auto">
        <div class="flex items-center justify-between">
          <div>
            <h2 class="text-xl font-bold text-gray-900 dark:text-white">
              Halo, Surya! 👋
            </h2>
            <p class="text-sm text-gray-600 dark:text-gray-300 mt-1">
              Rekomendasi AI siap untuk Anda
            </p>
          </div>
          <UBadge color="primary" size="lg" variant="subtle">
            <UIcon name="i-lucide-shield-check" class="mr-1" />
            100% Aman
          </UBadge>
        </div>

        <!-- AI Suggestion -->
        <UCard class="mt-4">
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-orange-100 dark:bg-orange-900 flex items-center justify-center">
              <UIcon name="i-lucide-sparkles" class="text-lg text-primary" />
            </div>
            <div class="flex-1">
              <p class="text-xs text-gray-500 dark:text-gray-400">
                AI Recommendation
              </p>
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                "Charger fast charging 33W untuk Samsung A54 Anda"
              </p>
            </div>
            <UButton size="xs" variant="soft" to="/produk">
              Lihat
            </UButton>
          </div>
        </UCard>
      </div>
    </section>

    <!-- Quick Actions -->
    <section class="px-4 py-5 max-w-4xl mx-auto">
      <div class="grid grid-cols-4 gap-3">
        <NuxtLink
          v-for="action in quickActions"
          :key="action.label"
          :to="action.to"
          class="flex flex-col items-center gap-2 p-3 rounded-xl bg-gray-50 dark:bg-gray-800 hover:bg-orange-50 dark:hover:bg-orange-900/30 transition-colors"
        >
          <div class="w-10 h-10 rounded-full bg-orange-100 dark:bg-orange-900 flex items-center justify-center">
            <UIcon :name="action.icon" class="text-lg text-primary" />
          </div>
          <span class="text-[10px] font-medium text-gray-700 dark:text-gray-300 text-center">{{ action.label }}</span>
        </NuxtLink>
      </div>
    </section>

    <!-- Rekomendasi AI -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <div class="flex items-center justify-between mb-3">
        <h3 class="font-semibold text-gray-900 dark:text-white flex items-center gap-2">
          <UIcon name="i-lucide-sparkles" class="text-primary" />
          Rekomendasi untuk Anda
        </h3>
        <NuxtLink to="/pencarian" class="text-xs text-primary font-medium">
          Lihat Semua →
        </NuxtLink>
      </div>
      <div class="grid grid-cols-2 gap-3">
        <NuxtLink
          v-for="product in recommendations"
          :key="product.id"
          to="/produk"
          class="block"
        >
          <UCard class="h-full hover:shadow-md transition-shadow">
            <div class="text-center text-3xl mb-2">
              {{ product.image }}
            </div>
            <p class="text-xs font-medium text-gray-900 dark:text-white line-clamp-2">
              {{ product.name }}
            </p>
            <p class="text-sm font-bold text-primary mt-1">
              {{ formatPrice(product.price) }}
            </p>
            <div class="flex items-center justify-between mt-2">
              <div class="flex items-center gap-1">
                <UIcon name="i-lucide-star" class="text-xs text-amber-500" />
                <span class="text-[10px] text-gray-500">{{ product.rating }}</span>
              </div>
              <UBadge size="xs" variant="subtle" color="success">
                Trust {{ product.trust }}
              </UBadge>
            </div>
            <p class="text-[10px] text-gray-400 mt-1">
              {{ product.sold.toLocaleString() }} terjual
            </p>
          </UCard>
        </NuxtLink>
      </div>
    </section>

    <!-- Flash Sale Terverifikasi -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <div class="flex items-center justify-between mb-3">
        <h3 class="font-semibold text-gray-900 dark:text-white flex items-center gap-2">
          <UIcon name="i-lucide-zap" class="text-red-500" />
          Flash Sale Terverifikasi
        </h3>
        <UBadge color="error" variant="subtle" size="xs">
          Berakhir 02:45:30
        </UBadge>
      </div>
      <div class="flex gap-3 overflow-x-auto pb-2">
        <NuxtLink
          v-for="item in flashSale"
          :key="item.id"
          to="/produk"
          class="shrink-0 w-36"
        >
          <UCard class="h-full hover:shadow-md transition-shadow">
            <div class="text-center text-2xl mb-2">
              {{ item.image }}
            </div>
            <p class="text-[10px] font-medium text-gray-900 dark:text-white line-clamp-2">
              {{ item.name }}
            </p>
            <p class="text-xs font-bold text-red-600 mt-1">
              {{ formatPrice(item.price) }}
            </p>
            <p class="text-[10px] text-gray-400 line-through">
              {{ formatPrice(item.originalPrice) }}
            </p>
            <UBadge size="xs" variant="subtle" color="success" class="mt-1">
              Trust {{ item.trust }}
            </UBadge>
          </UCard>
        </NuxtLink>
      </div>
    </section>

    <!-- Jaminan -->
    <section class="px-4 py-4 max-w-4xl mx-auto mb-4">
      <UCard variant="subtle" class="bg-green-50 dark:bg-green-950 border-green-200 dark:border-green-800">
        <div class="flex items-center gap-3">
          <UIcon name="i-lucide-shield-check" class="text-2xl text-green-600 shrink-0" />
          <div>
            <p class="font-semibold text-green-900 dark:text-green-100 text-sm">
              Jaminan Belanja Aman 100%
            </p>
            <p class="text-xs text-green-800 dark:text-green-200 mt-0.5">
              Uang kembali jika barang KW atau tidak sesuai deskripsi. Refund &lt; 48 jam.
            </p>
          </div>
        </div>
      </UCard>
    </section>
  </div>
</template>
