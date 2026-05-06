<script setup lang="ts">
const totalSetoran = ref(25)
const bulanIni = ref(8)
const totalPoin = ref(1250)

const jenisOptions = ['Organik', 'Plastik', 'Kertas/Kardus', 'Kaca', 'Logam', 'Elektronik', 'B3']

const formData = reactive({
  jenis: 'Organik',
  berat: '',
  catatan: ''
})

const riwayat = ref([
  { id: 1, tanggal: '5 Mei 2026', jenis: 'Plastik', berat: 2, poin: 50, status: 'Diterima' },
  { id: 2, tanggal: '3 Mei 2026', jenis: 'Organik', berat: 3, poin: 30, status: 'Diterima' },
  { id: 3, tanggal: '1 Mei 2026', jenis: 'Kertas/Kardus', berat: 4, poin: 60, status: 'Diterima' },
  { id: 4, tanggal: '28 Apr 2026', jenis: 'Plastik', berat: 1.5, poin: 38, status: 'Diterima' },
  { id: 5, tanggal: '25 Apr 2026', jenis: 'Organik', berat: 5, poin: 50, status: 'Diterima' }
])

const showForm = ref(false)

function submitSetoran() {
  if (formData.berat) {
    const poin = Math.round(parseFloat(formData.berat) * 25)
    riwayat.value.unshift({
      id: riwayat.value.length + 1,
      tanggal: new Date().toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric' }),
      jenis: formData.jenis,
      berat: parseFloat(formData.berat),
      poin,
      status: 'Menunggu Verifikasi'
    })
    totalSetoran.value += parseFloat(formData.berat)
    bulanIni.value += parseFloat(formData.berat)
    showForm.value = false
    formData.berat = ''
    formData.catatan = ''
  }
}

const poinPerKg: Record<string, number> = {
  'Organik': 10,
  'Plastik': 25,
  'Kertas/Kardus': 15,
  'Kaca': 20,
  'Logam': 30,
  'Elektronik': 50,
  'B3': 5
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <section class="bg-gradient-to-r from-red-50 to-rose-50 dark:from-red-950 dark:to-rose-950 px-4 py-6">
      <div class="max-w-4xl mx-auto">
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
          <UIcon
            name="i-lucide-recycle"
            class="text-primary"
          />
          Setor Sampah
        </h1>
        <p class="text-gray-600 dark:text-gray-300 mt-1">
          Catat dan kelola setoran sampah Anda
        </p>
      </div>
    </section>

    <!-- Stats -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <div class="grid grid-cols-3 gap-3">
        <UCard class="text-center !p-3">
          <p class="text-xl font-bold text-primary">
            {{ totalSetoran }}kg
          </p>
          <p class="text-xs text-gray-500">
            Total Setoran
          </p>
        </UCard>
        <UCard class="text-center !p-3">
          <p class="text-xl font-bold text-primary">
            {{ bulanIni }}kg
          </p>
          <p class="text-xs text-gray-500">
            Bulan Ini
          </p>
        </UCard>
        <UCard class="text-center !p-3">
          <p class="text-xl font-bold text-primary">
            {{ totalPoin.toLocaleString() }}
          </p>
          <p class="text-xs text-gray-500">
            Total Poin
          </p>
        </UCard>
      </div>
    </section>

    <!-- New Deposit Button -->
    <section class="px-4 py-2 max-w-4xl mx-auto">
      <UButton
        v-if="!showForm"
        color="primary"
        size="lg"
        icon="i-lucide-plus"
        class="w-full"
        @click="showForm = true"
      >
        Catat Setoran Baru
      </UButton>
    </section>

    <!-- Deposit Form -->
    <section
      v-if="showForm"
      class="px-4 py-2 max-w-4xl mx-auto"
    >
      <UCard>
        <div class="space-y-4">
          <h3 class="font-semibold text-gray-900 dark:text-white">
            Setoran Baru
          </h3>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Jenis Sampah</label>
            <select
              v-model="formData.jenis"
              class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
            >
              <option
                v-for="jenis in jenisOptions"
                :key="jenis"
                :value="jenis"
              >
                {{ jenis }}
              </option>
            </select>
            <p class="text-xs text-gray-500 mt-1">
              Poin: {{ poinPerKg[formData.jenis] }} per kg
            </p>
          </div>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Berat (kg)</label>
            <input
              v-model="formData.berat"
              type="number"
              step="0.1"
              min="0.1"
              placeholder="Masukkan berat dalam kg"
              class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
            >
          </div>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Catatan (opsional)</label>
            <textarea
              v-model="formData.catatan"
              rows="2"
              placeholder="Catatan tambahan..."
              class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
            />
          </div>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Foto (opsional)</label>
            <div class="border-2 border-dashed border-gray-300 dark:border-gray-600 rounded-lg p-6 text-center">
              <UIcon
                name="i-lucide-camera"
                class="text-3xl text-gray-400 mb-2"
              />
              <p class="text-sm text-gray-500">
                Tap untuk ambil foto sampah
              </p>
            </div>
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
              :disabled="!formData.berat"
              @click="submitSetoran"
            >
              Kirim Setoran
            </UButton>
          </div>
        </div>
      </UCard>
    </section>

    <!-- History -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">
        Riwayat Setoran
      </h2>
      <div class="space-y-2">
        <UCard
          v-for="item in riwayat"
          :key="item.id"
          class="!p-3"
        >
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-red-100 dark:bg-red-900 flex items-center justify-center">
              <UIcon
                name="i-lucide-recycle"
                class="text-primary"
              />
            </div>
            <div class="flex-1">
              <div class="flex items-center gap-2">
                <p class="text-sm font-medium text-gray-900 dark:text-white">
                  {{ item.jenis }}
                </p>
                <UBadge
                  :color="item.status === 'Diterima' ? 'success' : 'warning'"
                  variant="subtle"
                  size="xs"
                >
                  {{ item.status }}
                </UBadge>
              </div>
              <p class="text-xs text-gray-500">
                {{ item.tanggal }} • {{ item.berat }}kg
              </p>
            </div>
            <span class="text-sm font-bold text-red-600">+{{ item.poin }}</span>
          </div>
        </UCard>
      </div>
    </section>
  </div>
</template>
