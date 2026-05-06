<script setup lang="ts">
const user = reactive({
  nama: 'Budi Santoso',
  email: 'budi.santoso@email.com',
  telepon: '081234567890',
  alamat: 'Jl. Anggrek No. 15, RT 05 / RW 02',
  kelurahan: 'Cipinang Melayu',
  kecamatan: 'Makasar',
  kota: 'Jakarta Timur',
  bergabung: 'Januari 2026'
})

const stats = {
  totalSetoran: '25 kg',
  totalPoin: '1.250',
  laporanDibuat: 3,
  quizDijawab: 15,
  ranking: '#2 di RT 05'
}

const badges = [
  { name: 'Pemilah Pemula', icon: '🌱', earned: true },
  { name: 'Setoran Pertama', icon: '♻️', earned: true },
  { name: 'Quiz Master', icon: '🧠', earned: true },
  { name: 'Pelapor Aktif', icon: '📢', earned: true },
  { name: 'Eco Warrior', icon: '🌍', earned: false },
  { name: '100kg Club', icon: '💪', earned: false }
]

const notifSettings = reactive({
  jadwal: true,
  poin: true,
  laporan: true,
  komunitas: false,
  tips: true
})
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <section class="bg-gradient-to-r from-green-50 to-teal-50 dark:from-green-950 dark:to-teal-950 px-4 py-6">
      <div class="max-w-4xl mx-auto">
        <div class="flex items-center gap-4">
          <div class="w-16 h-16 rounded-full bg-green-200 dark:bg-green-800 flex items-center justify-center text-3xl">
            👨
          </div>
          <div>
            <h1 class="text-xl font-bold text-gray-900 dark:text-white">
              {{ user.nama }}
            </h1>
            <p class="text-sm text-gray-600 dark:text-gray-300">
              {{ user.alamat }}
            </p>
            <p class="text-xs text-gray-500 mt-1">
              Bergabung sejak {{ user.bergabung }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <div class="grid grid-cols-2 lg:grid-cols-5 gap-3">
        <UCard class="text-center !p-3">
          <p class="text-lg font-bold text-primary">
            {{ stats.totalSetoran }}
          </p>
          <p class="text-xs text-gray-500">
            Total Setoran
          </p>
        </UCard>
        <UCard class="text-center !p-3">
          <p class="text-lg font-bold text-primary">
            {{ stats.totalPoin }}
          </p>
          <p class="text-xs text-gray-500">
            Total Poin
          </p>
        </UCard>
        <UCard class="text-center !p-3">
          <p class="text-lg font-bold text-primary">
            {{ stats.laporanDibuat }}
          </p>
          <p class="text-xs text-gray-500">
            Laporan
          </p>
        </UCard>
        <UCard class="text-center !p-3">
          <p class="text-lg font-bold text-primary">
            {{ stats.quizDijawab }}
          </p>
          <p class="text-xs text-gray-500">
            Quiz
          </p>
        </UCard>
        <UCard class="text-center !p-3 col-span-2 lg:col-span-1">
          <p class="text-lg font-bold text-primary">
            {{ stats.ranking }}
          </p>
          <p class="text-xs text-gray-500">
            Ranking
          </p>
        </UCard>
      </div>
    </section>

    <!-- Badges -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">
        Badge & Pencapaian
      </h2>
      <div class="grid grid-cols-3 gap-3">
        <div
          v-for="badge in badges"
          :key="badge.name"
          class="text-center p-3 rounded-xl"
          :class="badge.earned
            ? 'bg-green-50 dark:bg-green-950 border border-green-200 dark:border-green-800'
            : 'bg-gray-50 dark:bg-gray-800 opacity-50'"
        >
          <span class="text-2xl">{{ badge.icon }}</span>
          <p
            class="text-xs font-medium mt-1"
            :class="badge.earned ? 'text-gray-900 dark:text-white' : 'text-gray-400'"
          >
            {{ badge.name }}
          </p>
          <UIcon
            v-if="badge.earned"
            name="i-lucide-check-circle"
            class="text-green-500 text-sm mt-1"
          />
          <UIcon
            v-else
            name="i-lucide-lock"
            class="text-gray-400 text-sm mt-1"
          />
        </div>
      </div>
    </section>

    <!-- Data Diri -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">
        Data Diri
      </h2>
      <UCard>
        <div class="space-y-3">
          <div class="flex justify-between items-center py-2 border-b border-gray-100 dark:border-gray-800">
            <span class="text-sm text-gray-500">Nama</span>
            <span class="text-sm font-medium text-gray-900 dark:text-white">{{ user.nama }}</span>
          </div>
          <div class="flex justify-between items-center py-2 border-b border-gray-100 dark:border-gray-800">
            <span class="text-sm text-gray-500">Email</span>
            <span class="text-sm font-medium text-gray-900 dark:text-white">{{ user.email }}</span>
          </div>
          <div class="flex justify-between items-center py-2 border-b border-gray-100 dark:border-gray-800">
            <span class="text-sm text-gray-500">Telepon</span>
            <span class="text-sm font-medium text-gray-900 dark:text-white">{{ user.telepon }}</span>
          </div>
          <div class="flex justify-between items-center py-2 border-b border-gray-100 dark:border-gray-800">
            <span class="text-sm text-gray-500">Kelurahan</span>
            <span class="text-sm font-medium text-gray-900 dark:text-white">{{ user.kelurahan }}</span>
          </div>
          <div class="flex justify-between items-center py-2">
            <span class="text-sm text-gray-500">Kota</span>
            <span class="text-sm font-medium text-gray-900 dark:text-white">{{ user.kota }}</span>
          </div>
        </div>
      </UCard>
    </section>

    <!-- Notification Settings -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">
        Pengaturan Notifikasi
      </h2>
      <UCard>
        <div class="space-y-4">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                Jadwal Penjemputan
              </p>
              <p class="text-xs text-gray-500">
                Pengingat H-1 dan hari H
              </p>
            </div>
            <input
              v-model="notifSettings.jadwal"
              type="checkbox"
              class="w-5 h-5 text-primary rounded"
            >
          </div>
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                Poin Masuk
              </p>
              <p class="text-xs text-gray-500">
                Notifikasi saat poin ditambahkan
              </p>
            </div>
            <input
              v-model="notifSettings.poin"
              type="checkbox"
              class="w-5 h-5 text-primary rounded"
            >
          </div>
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                Update Laporan
              </p>
              <p class="text-xs text-gray-500">
                Status laporan yang Anda buat
              </p>
            </div>
            <input
              v-model="notifSettings.laporan"
              type="checkbox"
              class="w-5 h-5 text-primary rounded"
            >
          </div>
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                Pengumuman Komunitas
              </p>
              <p class="text-xs text-gray-500">
                Berita & info dari pengelola
              </p>
            </div>
            <input
              v-model="notifSettings.komunitas"
              type="checkbox"
              class="w-5 h-5 text-primary rounded"
            >
          </div>
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                Tips Harian
              </p>
              <p class="text-xs text-gray-500">
                Tips pengelolaan sampah setiap hari
              </p>
            </div>
            <input
              v-model="notifSettings.tips"
              type="checkbox"
              class="w-5 h-5 text-primary rounded"
            >
          </div>
        </div>
      </UCard>
    </section>

    <!-- Logout -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <UButton
        color="error"
        variant="outline"
        class="w-full"
        icon="i-lucide-log-out"
      >
        Keluar dari Akun
      </UButton>
    </section>
  </div>
</template>
