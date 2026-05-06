<script setup lang="ts">
const currentMonth = ref('Mei 2026')

const schedules = ref([
  { id: 1, date: '7 Mei 2026', day: 'Rabu', time: '07:00', type: 'Organik', status: 'terjadwal', color: 'success' },
  { id: 2, date: '10 Mei 2026', day: 'Sabtu', time: '07:00', type: 'Anorganik', status: 'terjadwal', color: 'info' },
  { id: 3, date: '14 Mei 2026', day: 'Rabu', time: '07:00', type: 'Organik', status: 'terjadwal', color: 'success' },
  { id: 4, date: '17 Mei 2026', day: 'Sabtu', time: '07:00', type: 'Anorganik', status: 'terjadwal', color: 'info' },
  { id: 5, date: '21 Mei 2026', day: 'Rabu', time: '07:00', type: 'Organik', status: 'terjadwal', color: 'success' },
  { id: 6, date: '24 Mei 2026', day: 'Sabtu', time: '07:00', type: 'B3 / Khusus', status: 'terjadwal', color: 'error' },
  { id: 7, date: '28 Mei 2026', day: 'Rabu', time: '07:00', type: 'Organik', status: 'terjadwal', color: 'success' },
  { id: 8, date: '31 Mei 2026', day: 'Sabtu', time: '07:00', type: 'Anorganik', status: 'terjadwal', color: 'info' }
])

const confirmed = ref<number[]>([])

function confirmReady(id: number) {
  confirmed.value.push(id)
}

const typeColors: Record<string, string> = {
  'Organik': 'success',
  'Anorganik': 'info',
  'B3 / Khusus': 'error'
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <section class="bg-gradient-to-r from-red-50 to-blue-50 dark:from-red-950 dark:to-blue-950 px-4 py-6">
      <div class="max-w-4xl mx-auto">
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
          <UIcon
            name="i-lucide-calendar"
            class="text-primary"
          />
          Jadwal Penjemputan
        </h1>
        <p class="text-gray-600 dark:text-gray-300 mt-1">
          {{ currentMonth }}
        </p>
      </div>
    </section>

    <!-- Legend -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <div class="flex flex-wrap gap-3">
        <UBadge
          color="success"
          variant="subtle"
        >
          🟢 Organik
        </UBadge>
        <UBadge
          color="info"
          variant="subtle"
        >
          🔵 Anorganik
        </UBadge>
        <UBadge
          color="error"
          variant="subtle"
        >
          🔴 B3 / Khusus
        </UBadge>
      </div>
    </section>

    <!-- Schedule List -->
    <section class="px-4 py-2 max-w-4xl mx-auto">
      <div class="space-y-3">
        <UCard
          v-for="schedule in schedules"
          :key="schedule.id"
        >
          <div class="flex items-center gap-4">
            <!-- Date badge -->
            <div class="text-center min-w-[50px]">
              <p class="text-xs text-gray-500 uppercase">
                {{ schedule.day }}
              </p>
              <p class="text-lg font-bold text-gray-900 dark:text-white">
                {{ schedule.date.split(' ')[0] }}
              </p>
              <p class="text-xs text-gray-500">
                Mei
              </p>
            </div>

            <USeparator
              orientation="vertical"
              class="h-12"
            />

            <!-- Details -->
            <div class="flex-1">
              <div class="flex items-center gap-2">
                <UBadge
                  :color="typeColors[schedule.type] as any"
                  variant="subtle"
                  size="xs"
                >
                  {{ schedule.type }}
                </UBadge>
              </div>
              <p class="text-sm text-gray-600 dark:text-gray-300 mt-1">
                <UIcon
                  name="i-lucide-clock"
                  class="inline"
                /> {{ schedule.time }} WIB
              </p>
            </div>

            <!-- Action -->
            <div>
              <UButton
                v-if="!confirmed.includes(schedule.id)"
                size="sm"
                color="primary"
                variant="soft"
                @click="confirmReady(schedule.id)"
              >
                Siap
              </UButton>
              <UBadge
                v-else
                color="success"
                variant="solid"
              >
                <UIcon
                  name="i-lucide-check"
                  class="mr-1"
                />
                Dikonfirmasi
              </UBadge>
            </div>
          </div>
        </UCard>
      </div>
    </section>

    <!-- Info Box -->
    <section class="px-4 py-6 max-w-4xl mx-auto">
      <UCard
        variant="subtle"
        class="bg-blue-50 dark:bg-blue-950 border-blue-200 dark:border-blue-800"
      >
        <div class="flex items-start gap-3">
          <UIcon
            name="i-lucide-info"
            class="text-xl text-blue-500 shrink-0 mt-0.5"
          />
          <div>
            <p class="font-semibold text-blue-900 dark:text-blue-100">
              Informasi
            </p>
            <p class="text-sm text-blue-800 dark:text-blue-200 mt-1">
              Konfirmasi kesiapan setor agar petugas tahu rumah mana yang perlu didatangi. Jika tidak dikonfirmasi, petugas akan tetap lewat namun tidak berhenti.
            </p>
          </div>
        </div>
      </UCard>
    </section>
  </div>
</template>
