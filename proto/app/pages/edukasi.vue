<script setup lang="ts">
const activeTab = ref('panduan')

const categories = [
  {
    id: 'organik',
    name: 'Sampah Organik',
    icon: '🟢',
    color: 'success' as const,
    description: 'Sampah yang dapat terurai secara alami',
    examples: ['Sisa makanan', 'Kulit buah & sayuran', 'Daun kering', 'Ampas kopi/teh', 'Nasi basi', 'Tulang ayam/ikan'],
    tips: 'Masukkan ke wadah tertutup. Bisa dijadikan kompos dalam 2-4 minggu.',
    disposal: 'Wadah hijau / kompos'
  },
  {
    id: 'anorganik',
    name: 'Sampah Anorganik',
    icon: '🔵',
    color: 'info' as const,
    description: 'Sampah yang tidak mudah terurai, sebagian bisa didaur ulang',
    examples: ['Botol plastik', 'Kaleng aluminium', 'Kertas & kardus', 'Kaca/botol kaca', 'Plastik kemasan', 'Besi/logam'],
    tips: 'Bersihkan dari sisa makanan sebelum disetor. Pisahkan berdasarkan material.',
    disposal: 'Wadah biru / Bank Sampah'
  },
  {
    id: 'b3',
    name: 'Sampah B3 (Berbahaya)',
    icon: '🔴',
    color: 'error' as const,
    description: 'Sampah berbahaya & beracun, perlu penanganan khusus',
    examples: ['Baterai bekas', 'Lampu neon', 'Obat kedaluwarsa', 'Cat & tiner', 'Minyak pelumas bekas', 'Elektronik rusak'],
    tips: 'JANGAN dicampur dengan sampah lain. Simpan terpisah dan setor saat jadwal B3.',
    disposal: 'Wadah merah / pengumpulan khusus'
  }
]

const quizQuestions = [
  { question: 'Kulit jeruk termasuk sampah jenis apa?', options: ['Organik', 'Anorganik', 'B3'], answer: 0 },
  { question: 'Baterai bekas harus dibuang ke wadah warna?', options: ['Hijau', 'Biru', 'Merah'], answer: 2 },
  { question: 'Botol plastik bekas minuman termasuk?', options: ['Organik', 'Anorganik', 'B3'], answer: 1 },
  { question: 'Sisa nasi termasuk sampah?', options: ['Organik', 'Anorganik', 'B3'], answer: 0 },
  { question: 'Lampu neon pecah harus dibuang ke?', options: ['Wadah hijau', 'Wadah biru', 'Wadah merah (B3)'], answer: 2 }
]

const currentQuiz = ref(0)
const quizAnswer = ref<number | null>(null)
const quizSubmitted = ref(false)
const score = ref(0)

function submitAnswer() {
  if (quizAnswer.value === quizQuestions[currentQuiz.value]!.answer) {
    score.value++
  }
  quizSubmitted.value = true
}

function nextQuestion() {
  if (currentQuiz.value < quizQuestions.length - 1) {
    currentQuiz.value++
    quizAnswer.value = null
    quizSubmitted.value = false
  }
}
</script>

<template>
  <div class="pb-20 lg:pb-0">
    <!-- Header -->
    <section class="bg-gradient-to-r from-red-50 to-rose-50 dark:from-red-950 dark:to-rose-950 px-4 py-6">
      <div class="max-w-4xl mx-auto">
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
          <UIcon
            name="i-lucide-book-open"
            class="text-primary"
          />
          Edukasi Pemilahan Sampah
        </h1>
        <p class="text-gray-600 dark:text-gray-300 mt-1">
          Belajar memilah sampah dengan benar
        </p>
      </div>
    </section>

    <!-- Tabs -->
    <section class="px-4 py-4 max-w-4xl mx-auto">
      <UTabs
        v-model="activeTab"
        :items="[
          { label: 'Panduan', value: 'panduan', icon: 'i-lucide-book-open' },
          { label: 'Quiz', value: 'quiz', icon: 'i-lucide-brain' },
          { label: 'Scan', value: 'scan', icon: 'i-lucide-camera' }
        ]"
      />
    </section>

    <!-- Panduan Content -->
    <section
      v-if="activeTab === 'panduan'"
      class="px-4 py-2 max-w-4xl mx-auto"
    >
      <div class="space-y-4">
        <UCard
          v-for="category in categories"
          :key="category.id"
        >
          <div class="space-y-3">
            <div class="flex items-center gap-3">
              <span class="text-2xl">{{ category.icon }}</span>
              <div>
                <h3 class="font-bold text-gray-900 dark:text-white">
                  {{ category.name }}
                </h3>
                <p class="text-sm text-gray-500">
                  {{ category.description }}
                </p>
              </div>
            </div>

            <USeparator />

            <div>
              <p class="text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2">
                Contoh:
              </p>
              <div class="flex flex-wrap gap-2">
                <UBadge
                  v-for="example in category.examples"
                  :key="example"
                  :color="category.color"
                  variant="subtle"
                  size="sm"
                >
                  {{ example }}
                </UBadge>
              </div>
            </div>

            <UCard
              variant="subtle"
              class="!p-3 bg-gray-50 dark:bg-gray-800"
            >
              <p class="text-sm">
                <strong>💡 Tips:</strong> {{ category.tips }}
              </p>
              <p class="text-sm mt-1">
                <strong>🗑️ Buang ke:</strong> {{ category.disposal }}
              </p>
            </UCard>
          </div>
        </UCard>
      </div>
    </section>

    <!-- Quiz Content -->
    <section
      v-if="activeTab === 'quiz'"
      class="px-4 py-2 max-w-4xl mx-auto"
    >
      <UCard>
        <div class="space-y-4">
          <div class="flex items-center justify-between">
            <UBadge
              color="primary"
              variant="subtle"
            >
              Soal {{ currentQuiz + 1 }} / {{ quizQuestions.length }}
            </UBadge>
            <UBadge
              color="success"
              variant="subtle"
            >
              Skor: {{ score }}
            </UBadge>
          </div>

          <h3 class="text-lg font-semibold text-gray-900 dark:text-white">
            {{ quizQuestions[currentQuiz]!.question }}
          </h3>

          <div class="space-y-2">
            <button
              v-for="(option, idx) in quizQuestions[currentQuiz]!.options"
              :key="idx"
              class="w-full text-left p-3 rounded-lg border-2 transition-colors"
              :class="{
                'border-primary bg-red-50 dark:bg-red-950': quizAnswer === idx && !quizSubmitted,
                'border-red-500 bg-red-100 dark:bg-red-900': quizSubmitted && idx === quizQuestions[currentQuiz]!.answer,
                'border-red-500 bg-red-50 dark:bg-red-950': quizSubmitted && quizAnswer === idx && idx !== quizQuestions[currentQuiz]!.answer,
                'border-gray-200 dark:border-gray-700 hover:border-primary': !quizSubmitted && quizAnswer !== idx
              }"
              :disabled="quizSubmitted"
              @click="quizAnswer = idx"
            >
              {{ option }}
            </button>
          </div>

          <div class="flex gap-2">
            <UButton
              v-if="!quizSubmitted"
              color="primary"
              :disabled="quizAnswer === null"
              class="w-full"
              @click="submitAnswer"
            >
              Jawab
            </UButton>
            <UButton
              v-else-if="currentQuiz < quizQuestions.length - 1"
              color="primary"
              class="w-full"
              @click="nextQuestion"
            >
              Soal Berikutnya
            </UButton>
            <div
              v-else
              class="w-full text-center py-4"
            >
              <p class="text-lg font-bold text-primary">
                🎉 Quiz Selesai!
              </p>
              <p class="text-gray-600 dark:text-gray-300">
                Skor akhir: {{ score }} / {{ quizQuestions.length }}
              </p>
              <p class="text-sm text-gray-500 mt-1">
                +{{ score * 10 }} poin ditambahkan
              </p>
            </div>
          </div>
        </div>
      </UCard>
    </section>

    <!-- Scan Content -->
    <section
      v-if="activeTab === 'scan'"
      class="px-4 py-2 max-w-4xl mx-auto"
    >
      <UCard class="text-center">
        <div class="py-8 space-y-4">
          <div class="w-24 h-24 mx-auto rounded-full bg-gray-100 dark:bg-gray-800 flex items-center justify-center">
            <UIcon
              name="i-lucide-camera"
              class="text-4xl text-primary"
            />
          </div>
          <h3 class="text-lg font-semibold text-gray-900 dark:text-white">
            Scan Sampah
          </h3>
          <p class="text-gray-600 dark:text-gray-300 max-w-md mx-auto">
            Arahkan kamera ke sampah yang ingin Anda identifikasi. AI akan mendeteksi jenis sampah dan memberikan rekomendasi pembuangan.
          </p>
          <UButton
            color="primary"
            size="lg"
            icon="i-lucide-camera"
          >
            Buka Kamera
          </UButton>
          <p class="text-xs text-gray-400">
            * Fitur ini menggunakan AI untuk identifikasi visual
          </p>
        </div>
      </UCard>
    </section>
  </div>
</template>
