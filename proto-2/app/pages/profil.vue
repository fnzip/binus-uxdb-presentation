<script setup lang="ts">
const user = {
  name: 'Surya Angga',
  email: 'surya.angga@email.com',
  phone: '+62 812-xxxx-xxxx',
  address: 'Jl. Sudirman No. 123, Jakarta Selatan',
  member: 'Gold Member',
  joinDate: 'Januari 2023',
  totalOrders: 47,
  totalSpent: 8500000
}

const preferences = ref({
  aiRecommendation: true,
  priceAlert: true,
  verifiedOnly: true,
  darkMode: false
})

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
          Profil Saya
        </h1>
      </div>
    </header>

    <div class="max-w-4xl mx-auto px-4 py-4">
      <!-- Profile Card -->
      <UCard class="mb-4">
        <div class="flex items-center gap-4">
          <div class="w-16 h-16 rounded-full bg-orange-100 dark:bg-orange-900 flex items-center justify-center">
            <UIcon name="i-lucide-user" class="text-2xl text-primary" />
          </div>
          <div class="flex-1">
            <h2 class="text-base font-bold text-gray-900 dark:text-white">
              {{ user.name }}
            </h2>
            <UBadge color="warning" variant="subtle" size="xs" class="mt-1">
              {{ user.member }}
            </UBadge>
            <p class="text-xs text-gray-500 mt-1">
              Bergabung {{ user.joinDate }}
            </p>
          </div>
        </div>

        <!-- Stats -->
        <div class="grid grid-cols-2 gap-3 mt-4 pt-4 border-t border-gray-100 dark:border-gray-800">
          <div class="text-center">
            <p class="text-lg font-bold text-primary">{{ user.totalOrders }}</p>
            <p class="text-[10px] text-gray-500">Total Pesanan</p>
          </div>
          <div class="text-center">
            <p class="text-lg font-bold text-primary">{{ formatPrice(user.totalSpent) }}</p>
            <p class="text-[10px] text-gray-500">Total Belanja</p>
          </div>
        </div>
      </UCard>

      <!-- Personal Info -->
      <UCard class="mb-4">
        <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-3">
          Informasi Pribadi
        </h3>
        <div class="space-y-3">
          <div class="flex items-center gap-3">
            <UIcon name="i-lucide-mail" class="text-gray-400" />
            <div>
              <p class="text-[10px] text-gray-500">Email</p>
              <p class="text-xs text-gray-900 dark:text-white">{{ user.email }}</p>
            </div>
          </div>
          <div class="flex items-center gap-3">
            <UIcon name="i-lucide-phone" class="text-gray-400" />
            <div>
              <p class="text-[10px] text-gray-500">Telepon</p>
              <p class="text-xs text-gray-900 dark:text-white">{{ user.phone }}</p>
            </div>
          </div>
          <div class="flex items-center gap-3">
            <UIcon name="i-lucide-map-pin" class="text-gray-400" />
            <div>
              <p class="text-[10px] text-gray-500">Alamat</p>
              <p class="text-xs text-gray-900 dark:text-white">{{ user.address }}</p>
            </div>
          </div>
        </div>
      </UCard>

      <!-- AI Preferences -->
      <UCard class="mb-4">
        <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-3 flex items-center gap-1">
          <UIcon name="i-lucide-sparkles" class="text-primary" />
          Preferensi AI
        </h3>
        <div class="space-y-4">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-xs font-medium text-gray-900 dark:text-white">Rekomendasi AI</p>
              <p class="text-[10px] text-gray-500">Tampilkan produk relevan otomatis</p>
            </div>
            <USwitch v-model="preferences.aiRecommendation" />
          </div>
          <div class="flex items-center justify-between">
            <div>
              <p class="text-xs font-medium text-gray-900 dark:text-white">Alert Harga Turun</p>
              <p class="text-[10px] text-gray-500">Notifikasi saat harga produk diminati turun</p>
            </div>
            <USwitch v-model="preferences.priceAlert" />
          </div>
          <div class="flex items-center justify-between">
            <div>
              <p class="text-xs font-medium text-gray-900 dark:text-white">Hanya Produk Verified</p>
              <p class="text-[10px] text-gray-500">Filter otomatis seller Trust Score > 80</p>
            </div>
            <USwitch v-model="preferences.verifiedOnly" />
          </div>
        </div>
      </UCard>

      <!-- Help & Security -->
      <UCard>
        <h3 class="text-sm font-semibold text-gray-900 dark:text-white mb-3">
          Keamanan & Bantuan
        </h3>
        <div class="space-y-2">
          <div class="flex items-center gap-3 py-2">
            <UIcon name="i-lucide-shield" class="text-gray-400" />
            <span class="text-xs text-gray-900 dark:text-white flex-1">Keamanan Akun (2FA Aktif)</span>
            <UBadge size="xs" color="success" variant="subtle">Aman</UBadge>
          </div>
          <div class="flex items-center gap-3 py-2">
            <UIcon name="i-lucide-help-circle" class="text-gray-400" />
            <span class="text-xs text-gray-900 dark:text-white flex-1">Pusat Bantuan</span>
            <UIcon name="i-lucide-chevron-right" class="text-gray-400" />
          </div>
          <div class="flex items-center gap-3 py-2">
            <UIcon name="i-lucide-file-text" class="text-gray-400" />
            <span class="text-xs text-gray-900 dark:text-white flex-1">Kebijakan Privasi</span>
            <UIcon name="i-lucide-chevron-right" class="text-gray-400" />
          </div>
        </div>
      </UCard>
    </div>
  </div>
</template>
