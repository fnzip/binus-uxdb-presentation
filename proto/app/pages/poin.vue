<script setup lang="ts">
const saldo = ref(1250)
const nilaiRupiah = computed(() => saldo.value * 10)

const leaderboard = ref([
  { rank: 1, nama: 'Ibu Ani', poin: 3200, avatar: '👩' },
  { rank: 2, nama: 'Budi', poin: 1250, avatar: '👨', isMe: true },
  { rank: 3, nama: 'Pak Darto', poin: 980, avatar: '👴' },
  { rank: 4, nama: 'Mbak Rina', poin: 870, avatar: '👩‍🦱' },
  { rank: 5, nama: 'Mas Joko', poin: 750, avatar: '🧑' },
  { rank: 6, nama: 'Ibu Siti', poin: 620, avatar: '👩‍🦳' },
  { rank: 7, nama: 'Pak Heru', poin: 540, avatar: '👨‍🦰' },
  { rank: 8, nama: 'Dina', poin: 430, avatar: '👧' }
])

const riwayatPoin = ref([
  { id: 1, tanggal: '5 Mei 2026', keterangan: 'Setoran Plastik 2kg', jumlah: 50, tipe: 'masuk' },
  { id: 2, tanggal: '3 Mei 2026', keterangan: 'Setoran Organik 3kg', jumlah: 30, tipe: 'masuk' },
  { id: 3, tanggal: '2 Mei 2026', keterangan: 'Quiz Harian', jumlah: 10, tipe: 'masuk' },
  { id: 4, tanggal: '1 Mei 2026', keterangan: 'Setoran Kertas 4kg', jumlah: 60, tipe: 'masuk' },
  { id: 5, tanggal: '28 Apr 2026', keterangan: 'Tukar ke GoPay', jumlah: -500, tipe: 'keluar' },
  { id: 6, tanggal: '25 Apr 2026', keterangan: 'Setoran Organik 5kg', jumlah: 50, tipe: 'masuk' }
])

const ewalletOptions = [
  { name: 'GoPay', icon: '💚', min: 500 },
  { name: 'OVO', icon: '💜', min: 500 },
  { name: 'Dana', icon: '💙', min: 500 },
  { name: 'ShopeePay', icon: '🧡', min: 1000 }
]

const showRedeem = ref(false)
const selectedWallet = ref('')
const redeemAmount = ref('')

function tukarPoin() {
  const amount = parseInt(redeemAmount.value)
  if (amount && amount <= saldo.value && amount >= 500) {
    saldo.value -= amount
    riwayatPoin.value.unshift({
      id: riwayatPoin.value.length + 1,
      tanggal: new Date().toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric' }),
      keterangan: `Tukar ke ${selectedWallet.value}`,
      jumlah: -amount,
      tipe: 'keluar'
    })
    showRedeem.value = false
    redeemAmount.value = ''
    selectedWallet.value = ''
  }
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <section class="bg-gradient-to-r from-yellow-50 to-amber-50 dark:from-yellow-950 dark:to-amber-950 px-4 py-6">
      <div class="max-w-4xl mx-auto">
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
          <UIcon
            name="i-lucide-trophy"
            class="text-yellow-500"
          />
          Saku Digital
        </h1>
        <p class="text-gray-600 dark:text-gray-300 mt-1">
          EcoPoin & Leaderboard Komunitas
        </p>
      </div>
    </section>

    <!-- Balance Card -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <UCard class="bg-gradient-to-br from-red-500 to-rose-600 text-white">
        <div class="text-center py-4">
          <p class="text-sm opacity-80">
            Saldo EcoPoin
          </p>
          <p class="text-4xl font-bold mt-1">
            {{ saldo.toLocaleString() }}
          </p>
          <p class="text-sm opacity-80 mt-1">
            ≈ Rp {{ nilaiRupiah.toLocaleString() }}
          </p>
          <div class="flex gap-2 justify-center mt-4">
            <UButton
              color="neutral"
              variant="solid"
              size="sm"
              @click="showRedeem = !showRedeem"
            >
              <UIcon
                name="i-lucide-arrow-right-left"
                class="mr-1"
              />
              Tukar Poin
            </UButton>
            <UButton
              color="neutral"
              variant="outline"
              size="sm"
            >
              <UIcon
                name="i-lucide-history"
                class="mr-1"
              />
              Riwayat
            </UButton>
          </div>
        </div>
      </UCard>
    </section>

    <!-- Redeem Section -->
    <section
      v-if="showRedeem"
      class="px-4 py-2 max-w-4xl mx-auto"
    >
      <UCard>
        <div class="space-y-4">
          <h3 class="font-semibold text-gray-900 dark:text-white">
            Tukar Poin ke E-Wallet
          </h3>

          <div class="grid grid-cols-2 gap-2">
            <button
              v-for="wallet in ewalletOptions"
              :key="wallet.name"
              class="p-3 rounded-lg border-2 text-center transition-colors"
              :class="selectedWallet === wallet.name
                ? 'border-primary bg-red-50 dark:bg-red-950'
                : 'border-gray-200 dark:border-gray-700 hover:border-primary'"
              @click="selectedWallet = wallet.name"
            >
              <span class="text-2xl">{{ wallet.icon }}</span>
              <p class="text-sm font-medium mt-1">
                {{ wallet.name }}
              </p>
              <p class="text-xs text-gray-500">
                Min. {{ wallet.min }} poin
              </p>
            </button>
          </div>

          <div>
            <label class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-1 block">Jumlah Poin</label>
            <input
              v-model="redeemAmount"
              type="number"
              min="500"
              :max="saldo"
              step="100"
              placeholder="Minimum 500 poin"
              class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
            >
            <p class="text-xs text-gray-500 mt-1">
              Saldo tersedia: {{ saldo.toLocaleString() }} poin
            </p>
          </div>

          <UButton
            color="primary"
            class="w-full"
            :disabled="!selectedWallet || !redeemAmount || parseInt(redeemAmount) > saldo || parseInt(redeemAmount) < 500"
            @click="tukarPoin"
          >
            Tukar {{ redeemAmount ? parseInt(redeemAmount).toLocaleString() : '0' }} Poin
          </UButton>
        </div>
      </UCard>
    </section>

    <!-- Leaderboard -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white flex items-center gap-2">
        <UIcon
          name="i-lucide-trophy"
          class="text-yellow-500"
        />
        Leaderboard RT 05 — Mei 2026
      </h2>
      <UCard>
        <div class="space-y-2">
          <div
            v-for="user in leaderboard"
            :key="user.rank"
            class="flex items-center gap-3 p-2 rounded-lg"
            :class="user.isMe ? 'bg-red-50 dark:bg-red-950 border border-red-200 dark:border-red-800' : ''"
          >
            <span
              class="w-6 text-center font-bold"
              :class="{
                'text-yellow-500': user.rank === 1,
                'text-gray-400': user.rank === 2,
                'text-amber-600': user.rank === 3
              }"
            >
              {{ user.rank <= 3 ? ['🥇', '🥈', '🥉'][user.rank - 1] : `#${user.rank}` }}
            </span>
            <span class="text-xl">{{ user.avatar }}</span>
            <div class="flex-1">
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                {{ user.nama }}
                <UBadge
                  v-if="user.isMe"
                  color="primary"
                  variant="subtle"
                  size="xs"
                  class="ml-1"
                >
                  Anda
                </UBadge>
              </p>
            </div>
            <span class="text-sm font-bold text-primary">{{ user.poin.toLocaleString() }} pts</span>
          </div>
        </div>
      </UCard>
    </section>

    <!-- Transaction History -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <h2 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">
        Riwayat Poin
      </h2>
      <div class="space-y-2">
        <UCard
          v-for="trx in riwayatPoin"
          :key="trx.id"
          class="!p-3"
        >
          <div class="flex items-center gap-3">
            <div
              class="w-8 h-8 rounded-full flex items-center justify-center"
              :class="trx.tipe === 'masuk' ? 'bg-red-100 dark:bg-red-900' : 'bg-red-100 dark:bg-red-900'"
            >
              <UIcon
                :name="trx.tipe === 'masuk' ? 'i-lucide-arrow-down-left' : 'i-lucide-arrow-up-right'"
                :class="trx.tipe === 'masuk' ? 'text-red-600' : 'text-red-600'"
              />
            </div>
            <div class="flex-1">
              <p class="text-sm font-medium text-gray-900 dark:text-white">
                {{ trx.keterangan }}
              </p>
              <p class="text-xs text-gray-500">
                {{ trx.tanggal }}
              </p>
            </div>
            <span
              class="text-sm font-bold"
              :class="trx.tipe === 'masuk' ? 'text-red-600' : 'text-red-600'"
            >
              {{ trx.tipe === 'masuk' ? '+' : '' }}{{ trx.jumlah }}
            </span>
          </div>
        </UCard>
      </div>
    </section>
  </div>
</template>
