<script setup lang="ts">
const activeFilter = ref('semua')

const laporanList = ref([
  {
    id: 1,
    lokasi: 'Jl. Melati No. 5, RT 03',
    deskripsi: 'Tumpukan sampah besar di dekat selokan, berbau menyengat dan berpotensi menyumbat aliran air.',
    pelapor: 'Ibu Sari',
    tanggal: '4 Mei 2026',
    votes: 12,
    status: 'diproses',
    foto: true
  },
  {
    id: 2,
    lokasi: 'Taman RT 03, belakang pos ronda',
    deskripsi: 'Sampah plastik berserakan di area taman bermain anak. Perlu pembersihan segera.',
    pelapor: 'Pak Darto',
    tanggal: '3 Mei 2026',
    votes: 8,
    status: 'menunggu',
    foto: true
  },
  {
    id: 3,
    lokasi: 'Gang Kenanga No. 12',
    deskripsi: 'Ada pembuangan sampah elektronik (TV bekas, kipas angin rusak) yang ditinggalkan di pinggir jalan.',
    pelapor: 'Budi',
    tanggal: '2 Mei 2026',
    votes: 5,
    status: 'menunggu',
    foto: false
  },
  {
    id: 4,
    lokasi: 'Depan warung Bu Eko, Jl. Mawar',
    deskripsi: 'Tumpukan kardus dan plastik bekas jualan yang tidak diangkut seminggu lebih.',
    pelapor: 'Mas Joko',
    tanggal: '30 Apr 2026',
    votes: 15,
    status: 'selesai',
    foto: true
  },
  {
    id: 5,
    lokasi: 'Saluran air Jl. Dahlia',
    deskripsi: 'Sampah organik menyumbat saluran air, menyebabkan genangan saat hujan.',
    pelapor: 'Ibu Ani',
    tanggal: '28 Apr 2026',
    votes: 20,
    status: 'selesai',
    foto: true
  }
])

const filteredLaporan = computed(() => {
  if (activeFilter.value === 'semua') return laporanList.value
  return laporanList.value.filter(l => l.status === activeFilter.value)
})

const statusConfig: Record<string, { color: string, label: string }> = {
  menunggu: { color: 'warning', label: 'Menunggu' },
  diproses: { color: 'info', label: 'Diproses' },
  selesai: { color: 'success', label: 'Selesai' }
}

function upvote(id: number) {
  const laporan = laporanList.value.find(l => l.id === id)
  if (laporan) laporan.votes++
}

const showForm = ref(false)
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <section class="bg-gradient-to-r from-orange-50 to-red-50 dark:from-orange-950 dark:to-red-950 px-4 py-6">
      <div class="max-w-4xl mx-auto">
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
          <UIcon
            name="i-lucide-megaphone"
            class="text-orange-500"
          />
          Laporan Komunitas
        </h1>
        <p class="text-gray-600 dark:text-gray-300 mt-1">
          Laporkan tumpukan sampah di lingkungan Anda
        </p>
      </div>
    </section>

    <!-- Filter Tabs -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <div class="flex gap-2">
        <UButton
          v-for="tab in [
            { value: 'semua', label: 'Semua' },
            { value: 'menunggu', label: 'Menunggu' },
            { value: 'diproses', label: 'Diproses' },
            { value: 'selesai', label: 'Selesai' }
          ]"
          :key="tab.value"
          size="sm"
          :color="activeFilter === tab.value ? 'primary' : 'neutral'"
          :variant="activeFilter === tab.value ? 'solid' : 'outline'"
          @click="activeFilter = tab.value"
        >
          {{ tab.label }}
        </UButton>
      </div>
    </section>

    <!-- New Report Button -->
    <section class="px-4 py-2 max-w-4xl mx-auto">
      <UButton
        v-if="!showForm"
        color="primary"
        icon="i-lucide-plus"
        class="w-full"
        @click="showForm = true"
      >
        Buat Laporan Baru
      </UButton>
    </section>

    <!-- Report Form -->
    <section
      v-if="showForm"
      class="px-4 py-2 max-w-4xl mx-auto"
    >
      <UCard>
        <div class="space-y-4">
          <h3 class="font-semibold text-gray-900 dark:text-white">
            Laporan Baru
          </h3>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Lokasi</label>
            <input
              type="text"
              placeholder="Contoh: Jl. Melati No. 5, RT 03"
              class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
            >
          </div>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Deskripsi Masalah</label>
            <textarea
              rows="3"
              placeholder="Jelaskan masalah sampah yang Anda temui..."
              class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
            />
          </div>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Foto Bukti</label>
            <div class="border-2 border-dashed border-gray-300 dark:border-gray-600 rounded-lg p-6 text-center">
              <UIcon
                name="i-lucide-camera"
                class="text-3xl text-gray-400 mb-2"
              />
              <p class="text-sm text-gray-500">
                Tap untuk ambil foto lokasi
              </p>
            </div>
          </div>

          <div class="flex items-center gap-2 p-3 bg-blue-50 dark:bg-blue-950 rounded-lg">
            <UIcon
              name="i-lucide-map-pin"
              class="text-blue-500"
            />
            <p class="text-sm text-blue-700 dark:text-blue-300">
              Lokasi GPS akan otomatis ditandai
            </p>
          </div>

          <div class="flex gap-2">
            <UButton
              color="neutral"
              variant="outline"
              class="flex-1"
              @click="showForm = false"
            >
              Batal
            </UButton>
            <UButton
              color="primary"
              class="flex-1"
            >
              Kirim Laporan
            </UButton>
          </div>
        </div>
      </UCard>
    </section>

    <!-- Reports List -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <div class="space-y-3">
        <UCard
          v-for="laporan in filteredLaporan"
          :key="laporan.id"
        >
          <div class="space-y-3">
            <div class="flex items-start justify-between">
              <div class="flex items-center gap-2">
                <UIcon
                  name="i-lucide-map-pin"
                  class="text-red-500"
                />
                <span class="font-medium text-sm text-gray-900 dark:text-white">{{ laporan.lokasi }}</span>
              </div>
              <UBadge
                :color="statusConfig[laporan.status]?.color as any"
                variant="subtle"
                size="xs"
              >
                {{ statusConfig[laporan.status]?.label }}
              </UBadge>
            </div>

            <p class="text-sm text-gray-600 dark:text-gray-300">
              {{ laporan.deskripsi }}
            </p>

            <div
              v-if="laporan.foto"
              class="w-full h-32 bg-gray-100 dark:bg-gray-800 rounded-lg flex items-center justify-center"
            >
              <UIcon
                name="i-lucide-image"
                class="text-3xl text-gray-400"
              />
              <span class="text-sm text-gray-400 ml-2">Foto bukti</span>
            </div>

            <div class="flex items-center justify-between pt-2 border-t border-gray-100 dark:border-gray-800">
              <div class="flex items-center gap-3 text-xs text-gray-500">
                <span>{{ laporan.pelapor }}</span>
                <span>{{ laporan.tanggal }}</span>
              </div>
              <UButton
                size="xs"
                color="neutral"
                variant="outline"
                icon="i-lucide-thumbs-up"
                @click="upvote(laporan.id)"
              >
                {{ laporan.votes }}
              </UButton>
            </div>
          </div>
        </UCard>
      </div>
    </section>
  </div>
</template>
