<script setup lang="ts">
const orders = [
  {
    id: 'SHP-20260506-1234',
    status: 'Dalam Pengiriman',
    statusColor: 'primary' as const,
    product: 'Anker Nano 33W Fast Charger',
    image: '⚡',
    price: 150000,
    courier: 'J&T Express',
    eta: 'Besok, 09:00 WIB',
    timeline: [
      { time: '06 Mei 21:05', text: 'Pesanan dikonfirmasi', done: true },
      { time: '06 Mei 21:30', text: 'Sedang dikemas oleh seller', done: true },
      { time: '06 Mei 22:00', text: 'Diserahkan ke kurir J&T', done: true },
      { time: '07 Mei (est)', text: 'Dalam perjalanan ke alamat Anda', done: false }
    ]
  },
  {
    id: 'SHP-20260503-0987',
    status: 'Selesai',
    statusColor: 'success' as const,
    product: 'Samsung Silicone Case A54',
    image: '📱',
    price: 50000,
    courier: 'JNE',
    eta: 'Diterima 4 Mei 2026',
    timeline: [
      { time: '03 Mei 14:00', text: 'Pesanan dikonfirmasi', done: true },
      { time: '03 Mei 15:00', text: 'Dikemas', done: true },
      { time: '03 Mei 18:00', text: 'Dikirim', done: true },
      { time: '04 Mei 10:30', text: 'Diterima', done: true }
    ]
  }
]

const selectedOrder = ref(orders[0])
const showDetail = ref(false)

function formatPrice(price: number) {
  return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', minimumFractionDigits: 0 }).format(price)
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <header class="sticky top-0 z-40 bg-white dark:bg-gray-900 border-b border-gray-200 dark:border-gray-800 px-4 py-3">
      <div class="max-w-4xl mx-auto flex items-center gap-3">
        <NuxtLink to="/">
          <UIcon name="i-lucide-arrow-left" class="text-xl text-gray-600" />
        </NuxtLink>
        <h1 class="text-base font-semibold text-gray-900 dark:text-white">
          Pesanan Saya
        </h1>
      </div>
    </header>

    <div class="max-w-4xl mx-auto px-4 py-4">
      <!-- Order Detail View -->
      <div v-if="showDetail">
        <UButton variant="ghost" size="xs" icon="i-lucide-arrow-left" class="mb-3" @click="showDetail = false">
          Kembali ke daftar
        </UButton>

        <!-- Tracking Map Placeholder -->
        <UCard class="mb-4 bg-blue-50 dark:bg-blue-950">
          <div class="text-center py-6">
            <UIcon name="i-lucide-map" class="text-4xl text-blue-500 mb-2" />
            <p class="text-sm font-medium text-blue-900 dark:text-blue-100">Tracking Live</p>
            <p class="text-xs text-blue-700 dark:text-blue-300 mt-1">
              Kurir {{ selectedOrder.courier }} sedang menuju alamat Anda
            </p>
            <UBadge color="info" variant="subtle" class="mt-2">
              ETA: {{ selectedOrder.eta }}
            </UBadge>
          </div>
        </UCard>

        <!-- Product Info -->
        <UCard class="mb-4 !p-3">
          <div class="flex items-center gap-3">
            <div class="w-12 h-12 bg-gray-100 dark:bg-gray-800 rounded-lg flex items-center justify-center text-2xl">
              {{ selectedOrder.image }}
            </div>
            <div class="flex-1">
              <p class="text-xs font-medium text-gray-900 dark:text-white">{{ selectedOrder.product }}</p>
              <p class="text-xs text-primary font-bold mt-0.5">{{ formatPrice(selectedOrder.price) }}</p>
            </div>
            <UBadge :color="selectedOrder.statusColor" variant="subtle" size="xs">
              {{ selectedOrder.status }}
            </UBadge>
          </div>
        </UCard>

        <!-- Timeline -->
        <UCard>
          <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-4">
            Status Pengiriman
          </h3>
          <div class="space-y-4">
            <div v-for="(step, i) in selectedOrder.timeline" :key="i" class="flex gap-3">
              <div class="flex flex-col items-center">
                <div
                  class="w-6 h-6 rounded-full flex items-center justify-center shrink-0"
                  :class="step.done ? 'bg-green-100 dark:bg-green-900' : 'bg-gray-100 dark:bg-gray-800'"
                >
                  <UIcon
                    :name="step.done ? 'i-lucide-check' : 'i-lucide-circle'"
                    :class="step.done ? 'text-green-600 text-xs' : 'text-gray-400 text-xs'"
                  />
                </div>
                <div v-if="i < selectedOrder.timeline.length - 1" class="w-0.5 h-6 bg-gray-200 dark:bg-gray-700 mt-1" />
              </div>
              <div>
                <p class="text-xs font-medium text-gray-900 dark:text-white">{{ step.text }}</p>
                <p class="text-[10px] text-gray-500">{{ step.time }}</p>
              </div>
            </div>
          </div>
        </UCard>

        <!-- Guarantee -->
        <UCard variant="subtle" class="mt-4 bg-green-50 dark:bg-green-950 border-green-200 dark:border-green-800 !p-3">
          <div class="flex items-center gap-2">
            <UIcon name="i-lucide-shield-check" class="text-green-600" />
            <span class="text-xs text-green-800 dark:text-green-200">Dilindungi Jaminan 100% ShopSync</span>
          </div>
        </UCard>
      </div>

      <!-- Order List View -->
      <div v-else class="space-y-3">
        <UCard
          v-for="order in orders"
          :key="order.id"
          class="!p-3 cursor-pointer hover:shadow-md transition-shadow"
          @click="selectedOrder = order; showDetail = true"
        >
          <div class="flex items-center gap-3">
            <div class="w-12 h-12 bg-gray-100 dark:bg-gray-800 rounded-lg flex items-center justify-center text-2xl shrink-0">
              {{ order.image }}
            </div>
            <div class="flex-1 min-w-0">
              <p class="text-xs font-medium text-gray-900 dark:text-white truncate">
                {{ order.product }}
              </p>
              <p class="text-[10px] text-gray-500 mt-0.5">
                {{ order.id }} • {{ order.courier }}
              </p>
              <p class="text-xs text-primary font-bold mt-1">
                {{ formatPrice(order.price) }}
              </p>
            </div>
            <div class="text-right shrink-0">
              <UBadge :color="order.statusColor" variant="subtle" size="xs">
                {{ order.status }}
              </UBadge>
              <p class="text-[10px] text-gray-500 mt-1">
                {{ order.eta }}
              </p>
            </div>
          </div>
        </UCard>
      </div>
    </div>
  </div>
</template>
