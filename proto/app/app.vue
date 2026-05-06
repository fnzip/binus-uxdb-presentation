<script setup lang="ts">
useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico' }
  ],
  htmlAttrs: {
    lang: 'id'
  }
})

const title = 'EcoLink Community'
const description = 'Platform kolaboratif manajemen sampah komunitas — jadwal, edukasi, poin reward, dan laporan.'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description
})

const navItems = [
  { label: 'Home', to: '/', icon: 'i-lucide-home' },
  { label: 'Jadwal', to: '/jadwal', icon: 'i-lucide-calendar' },
  { label: 'Edukasi', to: '/edukasi', icon: 'i-lucide-book-open' },
  { label: 'Setor', to: '/setor', icon: 'i-lucide-recycle' },
  { label: 'Laporan', to: '/laporan', icon: 'i-lucide-megaphone' },
  { label: 'Poin', to: '/poin', icon: 'i-lucide-trophy' }
]
</script>

<template>
  <UApp>
    <UHeader>
      <template #left>
        <NuxtLink
          to="/"
          class="flex items-center gap-2"
        >
          <UIcon
            name="i-lucide-leaf"
            class="text-primary text-xl"
          />
          <span class="font-bold text-lg">EcoLink</span>
        </NuxtLink>
      </template>

      <template #body>
        <UNavigationMenu
          :items="navItems"
          class="hidden lg:flex"
        />
      </template>

      <template #right>
        <UButton
          to="/profil"
          icon="i-lucide-user"
          aria-label="Profil"
          color="neutral"
          variant="ghost"
        />
        <UColorModeButton />
      </template>
    </UHeader>

    <UMain>
      <NuxtPage />
    </UMain>

    <!-- Mobile Bottom Navigation -->
    <div class="fixed bottom-0 left-0 right-0 bg-white dark:bg-gray-900 border-t border-gray-200 dark:border-gray-800 lg:hidden z-50">
      <nav class="flex justify-around items-center py-2 px-1 max-w-lg mx-auto">
        <NuxtLink
          v-for="item in navItems"
          :key="item.to"
          :to="item.to"
          class="flex flex-col items-center gap-0.5 px-2 py-1 rounded-lg text-xs text-gray-500 hover:text-primary transition-colors"
          active-class="!text-primary font-semibold"
        >
          <UIcon
            :name="item.icon"
            class="text-lg"
          />
          <span>{{ item.label }}</span>
        </NuxtLink>
      </nav>
    </div>

    <USeparator
      icon="i-lucide-leaf"
      class="hidden lg:flex"
    />

    <UFooter class="hidden lg:flex">
      <template #left>
        <p class="text-sm text-muted">
          EcoLink Community © {{ new Date().getFullYear() }} — Platform Manajemen Sampah Komunitas
        </p>
      </template>
    </UFooter>
  </UApp>
</template>
