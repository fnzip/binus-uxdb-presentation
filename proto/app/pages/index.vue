<script setup lang="ts">
const poin = ref(1250)
const nextSchedule = {
  date: 'Rabu, 7 Mei 2026',
  time: '07:00 WIB',
  type: 'Sampah Organik',
  status: 'Terjadwal'
}

const quickActions = [
  { label: 'Jadwal', icon: 'i-lucide-calendar', to: '/jadwal', color: 'primary' as const },
  { label: 'Edukasi', icon: 'i-lucide-book-open', to: '/edukasi', color: 'primary' as const },
  { label: 'Setor', icon: 'i-lucide-recycle', to: '/setor', color: 'primary' as const },
  { label: 'Laporan', icon: 'i-lucide-megaphone', to: '/laporan', color: 'primary' as const }
]

const tips = [
  'Kulit pisang bisa jadi kompos dalam 2 minggu! 🍌',
  'Botol plastik yang bersih bernilai lebih tinggi di Bank Sampah.',
  'Minyak jelantah jangan dibuang ke selokan — bisa didaur ulang jadi biodiesel!',
  'Pisahkan tutup botol dari botolnya — keduanya didaur ulang berbeda.'
]

const todayTip = tips[new Date().getDay() % tips.length]

const recentActivity = [
  { icon: 'i-lucide-recycle', text: 'Setoran plastik 2kg diterima', time: '2 jam lalu', poin: '+50' },
  { icon: 'i-lucide-calendar', text: 'Jadwal organik besok 07:00', time: '5 jam lalu', poin: '' },
  { icon: 'i-lucide-trophy', text: 'Naik ke peringkat #2 RT 05', time: 'Kemarin', poin: '' }
]
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Hero Section -->
    <section class="bg-gradient-to-br from-red-50 to-rose-100 dark:from-red-950 dark:to-rose-900 px-4 py-8 lg:py-12">
      <div class="max-w-4xl mx-auto">
        <div class="flex items-center justify-between mb-4">
          <div>
            <h1 class="text-2xl lg:text-3xl font-bold text-gray-900 dark:text-white">
              Halo, Budi! 👋
            </h1>
            <p class="text-gray-600 dark:text-gray-300 mt-1">
              Selamat datang di EcoLink Community
            </p>
          </div>
          <div class="text-right">
            <UBadge
              color="primary"
              size="lg"
              variant="subtle"
            >
              <UIcon
                name="i-lucide-coins"
                class="mr-1"
              />
              {{ poin.toLocaleString() }} Poin
            </UBadge>
          </div>
        </div>

        <!-- Next Schedule Card -->
        <UCard class="mt-4">
          <div class="flex items-center gap-3">
            <div class="w-12 h-12 rounded-full bg-red-100 dark:bg-red-900 flex items-center justify-center">
              <UIcon
                name="i-lucide-truck"
                class="text-2xl text-primary"
              />
            </div>
            <div class="flex-1">
              <p class="text-sm text-gray-500 dark:text-gray-400">
                Penjemputan Berikutnya
              </p>
              <p class="font-semibold text-gray-900 dark:text-white">
                {{ nextSchedule.date }} — {{ nextSchedule.time }}
              </p>
              <p class="text-sm text-gray-600 dark:text-gray-300">
                {{ nextSchedule.type }}
              </p>
            </div>
            <UBadge
              color="success"
              variant="subtle"
            >
              {{ nextSchedule.status }}
            </UBadge>
          </div>
        </UCard>
      </div>
    </section>

    <!-- Quick Actions -->
    <section class="px-4 py-6 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-4 text-gray-900 dark:text-white">
        Aksi Cepat
      </h2>
      <div class="grid grid-cols-4 gap-3">
        <NuxtLink
          v-for="action in quickActions"
          :key="action.label"
          :to="action.to"
          class="flex flex-col items-center gap-2 p-3 rounded-xl bg-gray-50 dark:bg-gray-800 hover:bg-red-50 dark:hover:bg-red-900 transition-colors"
        >
          <div class="w-12 h-12 rounded-full bg-red-100 dark:bg-red-900 flex items-center justify-center">
            <UIcon
              :name="action.icon"
              class="text-xl text-primary"
            />
          </div>
          <span class="text-xs font-medium text-gray-700 dark:text-gray-300">{{ action.label }}</span>
        </NuxtLink>
      </div>
    </section>

    <!-- Tips Section -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <UCard
        variant="subtle"
        class="bg-amber-50 dark:bg-amber-950 border-amber-200 dark:border-amber-800"
      >
        <div class="flex items-start gap-3">
          <UIcon
            name="i-lucide-lightbulb"
            class="text-2xl text-amber-500 shrink-0 mt-0.5"
          />
          <div>
            <p class="font-semibold text-amber-900 dark:text-amber-100">
              Tips Hari Ini
            </p>
            <p class="text-sm text-amber-800 dark:text-amber-200 mt-1">
              {{ todayTip }}
            </p>
          </div>
        </div>
      </UCard>
    </section>

    <!-- Recent Activity -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-4 text-gray-900 dark:text-white">
        Aktivitas Terbaru
      </h2>
      <div class="space-y-3">
        <UCard
          v-for="(activity, index) in recentActivity"
          :key="index"
          class="!p-3"
        >
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-gray-100 dark:bg-gray-800 flex items-center justify-center">
              <UIcon
                :name="activity.icon"
                class="text-lg text-primary"
              />
            </div>
            <div class="flex-1">
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                {{ activity.text }}
              </p>
              <p class="text-xs text-gray-500">
                {{ activity.time }}
              </p>
            </div>
            <span
              v-if="activity.poin"
              class="text-sm font-bold text-red-600"
            >{{ activity.poin }}</span>
          </div>
        </UCard>
      </div>
    </section>

    <!-- Stats Overview -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-4 text-gray-900 dark:text-white">
        Dampak Lingkunganmu
      </h2>
      <div class="grid grid-cols-3 gap-3">
        <UCard class="text-center !p-4">
          <p class="text-2xl font-bold text-primary">
            25
          </p>
          <p class="text-xs text-gray-500 mt-1">
            kg sampah terkelola
          </p>
        </UCard>
        <UCard class="text-center !p-4">
          <p class="text-2xl font-bold text-primary">
            12
          </p>
          <p class="text-xs text-gray-500 mt-1">
            kg CO₂ tersimpan
          </p>
        </UCard>
        <UCard class="text-center !p-4">
          <p class="text-2xl font-bold text-primary">
            3
          </p>
          <p class="text-xs text-gray-500 mt-1">
            pohon diselamatkan
          </p>
        </UCard>
      </div>
    </section>
  </div>
</template>
