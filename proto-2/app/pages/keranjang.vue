<script setup lang="ts">
const cartItems = ref([
  { id: 1, name: 'Anker Nano 33W Fast Charger USB-C', price: 150000, qty: 1, image: '⚡', seller: 'TechStore Official', trust: 95 },
  { id: 2, name: 'Samsung Silicone Case Galaxy A54', price: 50000, qty: 1, image: '📱', seller: 'Samsung Official', trust: 92 }
])

const voucher = ref('Gratis Ongkir J&T')
const step = ref(1)

const subtotal = computed(() => cartItems.value.reduce((sum, item) => sum + (item.price * item.qty), 0))
const shipping = 0
const total = computed(() => subtotal.value + shipping)

const paymentMethods = [
  { label: 'ShopeePay', icon: 'i-lucide-wallet', balance: 'Rp 500.000' },
  { label: 'Transfer Bank', icon: 'i-lucide-landmark', balance: '' },
  { label: 'COD', icon: 'i-lucide-banknote', balance: '' },
  { label: 'PayLater', icon: 'i-lucide-clock', balance: 'Limit Rp 2.000.000' }
]

const selectedPayment = ref('ShopeePay')
const orderConfirmed = ref(false)

function removeItem(id: number) {
  cartItems.value = cartItems.value.filter(i => i.id !== id)
}

function confirmOrder() {
  orderConfirmed.value = true
}

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
          {{ orderConfirmed ? 'Pesanan Dikonfirmasi' : step === 1 ? 'Keranjang Belanja' : step === 2 ? 'Pilih Pembayaran' : 'Konfirmasi' }}
        </h1>
      </div>
    </header>

    <!-- Order Confirmed -->
    <div v-if="orderConfirmed" class="max-w-4xl mx-auto px-4 py-12 text-center">
      <div class="w-20 h-20 rounded-full bg-green-100 dark:bg-green-900 flex items-center justify-center mx-auto mb-4">
        <UIcon name="i-lucide-check-circle" class="text-4xl text-green-600" />
      </div>
      <h2 class="text-xl font-bold text-gray-900 dark:text-white">
        Pesanan Berhasil!
      </h2>
      <p class="text-sm text-gray-500 mt-2">
        Pesanan #SHP-20260506-1234 sedang diproses
      </p>
      <UBadge color="success" variant="subtle" size="lg" class="mt-3">
        <UIcon name="i-lucide-shield-check" class="mr-1" />
        Dilindungi Jaminan 100%
      </UBadge>
      <div class="mt-6 space-y-3">
        <UButton to="/pesanan" block>
          Lacak Pesanan
        </UButton>
        <UButton to="/" variant="outline" block color="neutral">
          Kembali Belanja
        </UButton>
      </div>
    </div>

    <!-- Cart Step 1 -->
    <div v-else-if="step === 1" class="max-w-4xl mx-auto">
      <section class="px-4 py-4">
        <div v-if="cartItems.length === 0" class="text-center py-12">
          <UIcon name="i-lucide-shopping-cart" class="text-4xl text-gray-300 mb-3" />
          <p class="text-gray-500">Keranjang kosong</p>
          <UButton to="/" variant="soft" class="mt-4">
            Mulai Belanja
          </UButton>
        </div>

        <div v-else class="space-y-3">
          <UCard v-for="item in cartItems" :key="item.id" class="!p-3">
            <div class="flex items-start gap-3">
              <div class="w-14 h-14 bg-gray-100 dark:bg-gray-800 rounded-lg flex items-center justify-center text-2xl shrink-0">
                {{ item.image }}
              </div>
              <div class="flex-1 min-w-0">
                <p class="text-xs font-medium text-gray-900 dark:text-white line-clamp-2">
                  {{ item.name }}
                </p>
                <p class="text-[10px] text-gray-500 mt-0.5">
                  {{ item.seller }}
                </p>
                <div class="flex items-center justify-between mt-2">
                  <p class="text-sm font-bold text-primary">
                    {{ formatPrice(item.price) }}
                  </p>
                  <div class="flex items-center gap-2">
                    <UBadge size="xs" variant="subtle" color="success">
                      Trust {{ item.trust }}
                    </UBadge>
                    <UButton size="xs" variant="ghost" color="error" icon="i-lucide-trash-2" @click="removeItem(item.id)" />
                  </div>
                </div>
              </div>
            </div>
          </UCard>

          <!-- Voucher -->
          <UCard class="!p-3 bg-orange-50 dark:bg-orange-950">
            <div class="flex items-center gap-2">
              <UIcon name="i-lucide-ticket" class="text-primary" />
              <span class="text-xs font-medium text-gray-900 dark:text-white flex-1">{{ voucher }}</span>
              <UBadge size="xs" color="success">Aktif</UBadge>
            </div>
          </UCard>

          <!-- Summary -->
          <div class="space-y-2 pt-3 border-t border-gray-100 dark:border-gray-800">
            <div class="flex justify-between text-xs text-gray-600">
              <span>Subtotal ({{ cartItems.length }} item)</span>
              <span>{{ formatPrice(subtotal) }}</span>
            </div>
            <div class="flex justify-between text-xs text-gray-600">
              <span>Ongkos Kirim</span>
              <span class="text-green-600 font-medium">GRATIS</span>
            </div>
            <div class="flex justify-between text-sm font-bold text-gray-900 dark:text-white pt-2 border-t border-gray-100 dark:border-gray-800">
              <span>Total</span>
              <span class="text-primary">{{ formatPrice(total) }}</span>
            </div>
          </div>
        </div>
      </section>

      <!-- Checkout Button -->
      <div v-if="cartItems.length > 0" class="fixed bottom-16 lg:bottom-0 left-0 right-0 bg-white dark:bg-gray-900 border-t border-gray-200 dark:border-gray-800 px-4 py-3 z-30">
        <div class="max-w-4xl mx-auto flex items-center justify-between">
          <div>
            <p class="text-xs text-gray-500">Total</p>
            <p class="text-base font-bold text-primary">{{ formatPrice(total) }}</p>
          </div>
          <UButton size="lg" @click="step = 2">
            Checkout Express
          </UButton>
        </div>
      </div>
    </div>

    <!-- Payment Step 2 -->
    <div v-else-if="step === 2" class="max-w-4xl mx-auto px-4 py-4">
      <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-3">
        Alamat Pengiriman
      </h3>
      <UCard class="!p-3 mb-4">
        <div class="flex items-start gap-2">
          <UIcon name="i-lucide-map-pin" class="text-primary shrink-0 mt-0.5" />
          <div>
            <p class="text-xs font-medium text-gray-900 dark:text-white">Surya Angga</p>
            <p class="text-[10px] text-gray-500">Jl. Sudirman No. 123, Jakarta Selatan, DKI Jakarta, 12190</p>
          </div>
        </div>
      </UCard>

      <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-3">
        Metode Pembayaran
      </h3>
      <div class="space-y-2">
        <UCard
          v-for="method in paymentMethods"
          :key="method.label"
          class="!p-3 cursor-pointer"
          :class="selectedPayment === method.label ? 'ring-2 ring-primary' : ''"
          @click="selectedPayment = method.label"
        >
          <div class="flex items-center gap-3">
            <UIcon :name="method.icon" class="text-lg text-gray-600" />
            <div class="flex-1">
              <p class="text-xs font-medium text-gray-900 dark:text-white">{{ method.label }}</p>
              <p v-if="method.balance" class="text-[10px] text-gray-500">{{ method.balance }}</p>
            </div>
            <UIcon
              v-if="selectedPayment === method.label"
              name="i-lucide-check-circle"
              class="text-primary"
            />
          </div>
        </UCard>
      </div>

      <div class="mt-6 space-y-3">
        <UButton block size="lg" @click="step = 3">
          Lanjut ke Konfirmasi
        </UButton>
        <UButton block variant="outline" color="neutral" @click="step = 1">
          Kembali
        </UButton>
      </div>
    </div>

    <!-- Confirmation Step 3 -->
    <div v-else-if="step === 3" class="max-w-4xl mx-auto px-4 py-4">
      <UCard class="mb-4">
        <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-3">
          Ringkasan Pesanan
        </h3>
        <div class="space-y-2">
          <div v-for="item in cartItems" :key="item.id" class="flex justify-between text-xs">
            <span class="text-gray-600 dark:text-gray-400">{{ item.name }}</span>
            <span class="font-medium text-gray-900 dark:text-white">{{ formatPrice(item.price) }}</span>
          </div>
        </div>
        <div class="border-t border-gray-100 dark:border-gray-800 mt-3 pt-3">
          <div class="flex justify-between text-xs text-gray-600">
            <span>Pengiriman (J&T Express)</span>
            <span class="text-green-600">GRATIS</span>
          </div>
          <div class="flex justify-between text-sm font-bold mt-2">
            <span>Total</span>
            <span class="text-primary">{{ formatPrice(total) }}</span>
          </div>
        </div>
      </UCard>

      <UCard class="mb-4 !p-3">
        <div class="flex items-center gap-2">
          <UIcon name="i-lucide-wallet" class="text-primary" />
          <span class="text-xs font-medium text-gray-900 dark:text-white">{{ selectedPayment }}</span>
        </div>
      </UCard>

      <UCard variant="subtle" class="mb-4 bg-green-50 dark:bg-green-950 border-green-200 dark:border-green-800 !p-3">
        <div class="flex items-center gap-2">
          <UIcon name="i-lucide-shield-check" class="text-green-600" />
          <span class="text-xs text-green-800 dark:text-green-200">Dilindungi Jaminan 100% — Uang kembali jika barang tidak sesuai</span>
        </div>
      </UCard>

      <div class="space-y-3">
        <UButton block size="lg" @click="confirmOrder">
          <UIcon name="i-lucide-lock" class="mr-1" />
          Bayar {{ formatPrice(total) }}
        </UButton>
        <UButton block variant="outline" color="neutral" @click="step = 2">
          Kembali
        </UButton>
      </div>
    </div>
  </div>
</template>
