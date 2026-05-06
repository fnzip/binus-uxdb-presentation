<script setup lang="ts">
const product = {
  id: 1,
  name: 'Anker Nano 33W Fast Charger USB-C PD 3.0',
  price: 150000,
  originalPrice: 250000,
  rating: 4.9,
  totalReviews: 234,
  sold: 5200,
  trustScore: 95,
  seller: {
    name: 'TechStore Official',
    badge: 'Emas',
    rating: 4.9,
    responseRate: '98%',
    joined: '2020'
  },
  specs: [
    'Output: 33W USB-C PD 3.0',
    'Input: 100-240V AC',
    'Kompatibel: iPhone, Samsung, Xiaomi',
    'Ukuran: 3cm x 3cm x 3.5cm',
    'Berat: 45g'
  ],
  image: '⚡'
}

const reviews = [
  { id: 1, user: 'Andi P.', rating: 5, text: 'Fast charging mantap! Samsung A54 saya full charge 1 jam.', date: '3 Mei 2026', verified: true, hasPhoto: true },
  { id: 2, user: 'Dina S.', rating: 5, text: 'Kecil tapi powerful. Build quality bagus banget.', date: '1 Mei 2026', verified: true, hasPhoto: true },
  { id: 3, user: 'Rudi K.', rating: 4, text: 'Oke banget buat harganya. Agak panas saat charging lama tapi normal.', date: '28 Apr 2026', verified: true, hasPhoto: false }
]

const chatMessages = ref([
  { role: 'ai' as const, text: 'Halo! Saya AI assistant ShopSync. Ada yang bisa saya bantu tentang produk ini?' }
])
const chatInput = ref('')
const showChat = ref(false)

function sendChat() {
  if (!chatInput.value.trim()) return
  chatMessages.value.push({ role: 'user' as const, text: chatInput.value })
  const q = chatInput.value.toLowerCase()
  chatInput.value = ''

  setTimeout(() => {
    if (q.includes('samsung') || q.includes('a54') || q.includes('cocok')) {
      chatMessages.value.push({ role: 'ai', text: 'Ya, Anker Nano 33W support PD 3.0 yang kompatibel dengan Samsung A54. Charging dari 0-50% sekitar 30 menit. ✓' })
    } else if (q.includes('garansi') || q.includes('rusak')) {
      chatMessages.value.push({ role: 'ai', text: 'Produk ini memiliki garansi resmi 18 bulan dari Anker. Jika rusak dalam masa garansi, bisa klaim langsung melalui ShopSync Guarantee.' })
    } else {
      chatMessages.value.push({ role: 'ai', text: 'Anker Nano 33W adalah charger kompak dengan teknologi GaN. Bisa charging HP, tablet, bahkan laptop ringan. Trust Score 95/100 berdasarkan 234 ulasan verified.' })
    }
  }, 800)
}

function formatPrice(price: number) {
  return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', minimumFractionDigits: 0 }).format(price)
}

const addedToCart = ref(false)
function addToCart() {
  addedToCart.value = true
  setTimeout(() => { addedToCart.value = false }, 2000)
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <header class="sticky top-0 z-40 bg-white dark:bg-gray-900 border-b border-gray-200 dark:border-gray-800 px-4 py-3">
      <div class="max-w-4xl mx-auto flex items-center gap-3">
        <NuxtLink to="/pencarian">
          <UIcon name="i-lucide-arrow-left" class="text-xl text-gray-600" />
        </NuxtLink>
        <h1 class="text-sm font-semibold text-gray-900 dark:text-white flex-1 truncate">
          Detail Produk
        </h1>
        <NuxtLink to="/keranjang">
          <UIcon name="i-lucide-shopping-cart" class="text-xl text-gray-600" />
        </NuxtLink>
      </div>
    </header>

    <div class="max-w-4xl mx-auto">
      <!-- Product Image/Video -->
      <section class="bg-gray-100 dark:bg-gray-800 flex items-center justify-center py-12">
        <div class="text-center">
          <span class="text-7xl">{{ product.image }}</span>
          <p class="text-xs text-gray-500 mt-3 flex items-center justify-center gap-1">
            <UIcon name="i-lucide-rotate-3d" />
            Video 360° tersedia
          </p>
        </div>
      </section>

      <!-- Product Info -->
      <section class="px-4 py-4">
        <div class="flex items-start justify-between gap-2">
          <div class="flex-1">
            <p class="text-lg font-bold text-primary">
              {{ formatPrice(product.price) }}
            </p>
            <p class="text-xs text-gray-400 line-through">
              {{ formatPrice(product.originalPrice) }}
            </p>
          </div>
          <UBadge size="lg" variant="subtle" color="success">
            <UIcon name="i-lucide-shield-check" class="mr-1" />
            Trust {{ product.trustScore }}/100
          </UBadge>
        </div>

        <h2 class="text-base font-semibold text-gray-900 dark:text-white mt-3">
          {{ product.name }}
        </h2>

        <div class="flex items-center gap-3 mt-2">
          <div class="flex items-center gap-1">
            <UIcon name="i-lucide-star" class="text-sm text-amber-500" />
            <span class="text-sm font-medium">{{ product.rating }}</span>
            <span class="text-xs text-gray-500">({{ product.totalReviews }} ulasan)</span>
          </div>
          <span class="text-xs text-gray-400">|</span>
          <span class="text-xs text-gray-500">{{ product.sold.toLocaleString() }} terjual</span>
        </div>
      </section>

      <!-- Seller Info -->
      <section class="px-4 py-3 border-t border-gray-100 dark:border-gray-800">
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-full bg-orange-100 dark:bg-orange-900 flex items-center justify-center">
            <UIcon name="i-lucide-store" class="text-primary" />
          </div>
          <div class="flex-1">
            <p class="text-sm font-semibold text-gray-900 dark:text-white flex items-center gap-1">
              {{ product.seller.name }}
              <UBadge size="xs" color="warning" variant="subtle">{{ product.seller.badge }}</UBadge>
            </p>
            <p class="text-xs text-gray-500">
              Respon {{ product.seller.responseRate }} • Bergabung {{ product.seller.joined }}
            </p>
          </div>
        </div>
      </section>

      <!-- Specs -->
      <section class="px-4 py-3 border-t border-gray-100 dark:border-gray-800">
        <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-2">
          Spesifikasi
        </h3>
        <ul class="space-y-1">
          <li v-for="spec in product.specs" :key="spec" class="text-xs text-gray-600 dark:text-gray-400 flex items-start gap-2">
            <UIcon name="i-lucide-check" class="text-green-500 shrink-0 mt-0.5" />
            {{ spec }}
          </li>
        </ul>
      </section>

      <!-- Reviews -->
      <section class="px-4 py-3 border-t border-gray-100 dark:border-gray-800">
        <div class="flex items-center justify-between mb-3">
          <h3 class="text-sm font-semibold text-gray-900 dark:text-white flex items-center gap-1">
            Ulasan Verified
            <UIcon name="i-lucide-badge-check" class="text-blue-500" />
          </h3>
          <span class="text-xs text-gray-500">{{ product.totalReviews }} ulasan</span>
        </div>

        <div class="space-y-3">
          <UCard v-for="review in reviews" :key="review.id" class="!p-3">
            <div class="flex items-start gap-2">
              <div class="w-8 h-8 rounded-full bg-gray-200 dark:bg-gray-700 flex items-center justify-center shrink-0">
                <UIcon name="i-lucide-user" class="text-gray-500 text-sm" />
              </div>
              <div class="flex-1">
                <div class="flex items-center gap-2">
                  <span class="text-xs font-medium text-gray-900 dark:text-white">{{ review.user }}</span>
                  <UBadge v-if="review.verified" size="xs" color="info" variant="subtle">
                    <UIcon name="i-lucide-badge-check" class="mr-0.5" />
                    Verified
                  </UBadge>
                </div>
                <div class="flex items-center gap-0.5 mt-0.5">
                  <UIcon v-for="i in review.rating" :key="i" name="i-lucide-star" class="text-[10px] text-amber-500" />
                </div>
                <p class="text-xs text-gray-600 dark:text-gray-400 mt-1">
                  {{ review.text }}
                </p>
                <div class="flex items-center gap-2 mt-1">
                  <span class="text-[10px] text-gray-400">{{ review.date }}</span>
                  <UBadge v-if="review.hasPhoto" size="xs" variant="outline" color="neutral">
                    <UIcon name="i-lucide-image" class="mr-0.5" />
                    Foto
                  </UBadge>
                </div>
              </div>
            </div>
          </UCard>
        </div>
      </section>

      <!-- AI Chat -->
      <section v-if="showChat" class="px-4 py-3 border-t border-gray-100 dark:border-gray-800">
        <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-3 flex items-center gap-1">
          <UIcon name="i-lucide-sparkles" class="text-primary" />
          Chat AI Produk
        </h3>
        <div class="space-y-2 max-h-48 overflow-y-auto mb-3">
          <div
            v-for="(msg, i) in chatMessages"
            :key="i"
            :class="msg.role === 'user' ? 'text-right' : 'text-left'"
          >
            <span
              class="inline-block px-3 py-2 rounded-lg text-xs max-w-[80%]"
              :class="msg.role === 'user' ? 'bg-primary text-white' : 'bg-gray-100 dark:bg-gray-800 text-gray-900 dark:text-white'"
            >
              {{ msg.text }}
            </span>
          </div>
        </div>
        <form class="flex gap-2" @submit.prevent="sendChat">
          <UInput
            v-model="chatInput"
            placeholder="Tanya AI tentang produk ini..."
            size="sm"
            class="flex-1"
          />
          <UButton type="submit" size="sm" icon="i-lucide-send" />
        </form>
      </section>
    </div>

    <!-- Bottom Action Bar -->
    <div class="fixed bottom-16 lg:bottom-0 left-0 right-0 bg-white dark:bg-gray-900 border-t border-gray-200 dark:border-gray-800 px-4 py-3 z-30">
      <div class="max-w-4xl mx-auto flex items-center gap-3">
        <UButton
          variant="outline"
          color="primary"
          icon="i-lucide-sparkles"
          @click="showChat = !showChat"
        >
          Chat AI
        </UButton>
        <UButton
          class="flex-1"
          size="lg"
          :color="addedToCart ? 'success' : 'primary'"
          :icon="addedToCart ? 'i-lucide-check' : 'i-lucide-shopping-cart'"
          @click="addToCart"
        >
          {{ addedToCart ? 'Ditambahkan!' : 'Tambah ke Keranjang' }}
        </UButton>
      </div>
    </div>
  </div>
</template>
