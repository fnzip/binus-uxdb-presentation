<script setup lang="ts">
const route = useRoute()
const searchQuery = ref((route.query.q as string) || '')
const selectedFilter = ref('Semua')

const filters = ['Semua', 'Rating Tertinggi', 'Harga Terendah', 'Trust Score', 'Terbaru']

const allProducts = [
  { id: 1, name: 'Anker Nano 33W Fast Charger USB-C', price: 150000, rating: 4.9, sold: 5200, trust: 95, image: '⚡', category: 'Charger' },
  { id: 2, name: 'Baseus GaN 65W Charger 3-Port', price: 320000, rating: 4.8, sold: 2100, trust: 93, image: '⚡', category: 'Charger' },
  { id: 3, name: 'Samsung 25W Super Fast Charger Original', price: 180000, rating: 4.9, sold: 8900, trust: 97, image: '⚡', category: 'Charger' },
  { id: 4, name: 'Ugreen 30W USB-C Charger Mini', price: 95000, rating: 4.7, sold: 12000, trust: 88, image: '⚡', category: 'Charger' },
  { id: 5, name: 'Sony WF-1000XM5 True Wireless', price: 3200000, rating: 4.9, sold: 890, trust: 98, image: '🎧', category: 'Audio' },
  { id: 6, name: 'Samsung Galaxy Buds3 Pro', price: 2800000, rating: 4.8, sold: 1500, trust: 96, image: '🎧', category: 'Audio' },
  { id: 7, name: 'Xiaomi Power Bank 20000mAh 33W', price: 180000, rating: 4.8, sold: 15000, trust: 91, image: '🔋', category: 'Power Bank' },
  { id: 8, name: 'Samsung Silicone Case Galaxy A54', price: 50000, rating: 4.8, sold: 3100, trust: 92, image: '📱', category: 'Aksesoris' }
]

const filteredProducts = computed(() => {
  let products = [...allProducts]
  if (searchQuery.value) {
    const q = searchQuery.value.toLowerCase()
    products = products.filter(p => p.name.toLowerCase().includes(q) || p.category.toLowerCase().includes(q))
  }
  if (selectedFilter.value === 'Rating Tertinggi') {
    products.sort((a, b) => b.rating - a.rating)
  } else if (selectedFilter.value === 'Harga Terendah') {
    products.sort((a, b) => a.price - b.price)
  } else if (selectedFilter.value === 'Trust Score') {
    products.sort((a, b) => b.trust - a.trust)
  }
  return products
})

function formatPrice(price: number) {
  return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', minimumFractionDigits: 0 }).format(price)
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Search Header -->
    <header class="sticky top-0 z-40 bg-white dark:bg-gray-900 border-b border-gray-200 dark:border-gray-800 px-4 py-3">
      <div class="max-w-4xl mx-auto">
        <div class="flex items-center gap-2">
          <NuxtLink to="/">
            <UIcon name="i-lucide-arrow-left" class="text-xl text-gray-600" />
          </NuxtLink>
          <UInput
            v-model="searchQuery"
            placeholder="Cari produk dengan AI..."
            icon="i-lucide-sparkles"
            size="md"
            class="flex-1"
          />
        </div>

        <!-- AI Smart Filter -->
        <div class="flex gap-2 mt-3 overflow-x-auto pb-1">
          <UButton
            v-for="filter in filters"
            :key="filter"
            size="xs"
            :variant="selectedFilter === filter ? 'solid' : 'outline'"
            :color="selectedFilter === filter ? 'primary' : 'neutral'"
            class="shrink-0"
            @click="selectedFilter = filter"
          >
            {{ filter }}
          </UButton>
        </div>
      </div>
    </header>

    <!-- AI Info -->
    <section class="px-4 py-3 max-w-4xl mx-auto">
      <div class="flex items-center gap-2 text-xs text-gray-500">
        <UIcon name="i-lucide-sparkles" class="text-primary" />
        <span>AI menemukan <strong class="text-gray-900 dark:text-white">{{ filteredProducts.length }} produk terverifikasi</strong> untuk Anda</span>
      </div>
    </section>

    <!-- Results Grid -->
    <section class="px-4 max-w-4xl mx-auto">
      <div class="grid grid-cols-2 gap-3">
        <NuxtLink
          v-for="product in filteredProducts"
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
  </div>
</template>
