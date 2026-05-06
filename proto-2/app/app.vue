<script setup>
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

const title = 'ShopSync — Belanja Pintar'
const description = 'Fitur AI Smart Shopping untuk pengalaman belanja online yang pintar, cepat, dan terpercaya.'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description
})
</script>

<template>
  <UApp>
    <UMain>
      <NuxtPage />
    </UMain>

    <!-- Mobile Bottom Navigation -->
    <nav class="fixed bottom-0 left-0 right-0 bg-white dark:bg-gray-900 border-t border-gray-200 dark:border-gray-800 z-50 lg:hidden">
      <div class="flex items-center justify-around py-2">
        <NuxtLink
          to="/"
          class="flex flex-col items-center gap-1 px-3 py-1 text-gray-500 hover:text-primary"
          active-class="text-primary"
        >
          <UIcon name="i-lucide-home" class="text-xl" />
          <span class="text-[10px] font-medium">Home</span>
        </NuxtLink>
        <NuxtLink
          to="/pencarian"
          class="flex flex-col items-center gap-1 px-3 py-1 text-gray-500 hover:text-primary"
          active-class="text-primary"
        >
          <UIcon name="i-lucide-search" class="text-xl" />
          <span class="text-[10px] font-medium">Cari</span>
        </NuxtLink>
        <NuxtLink
          to="/keranjang"
          class="flex flex-col items-center gap-1 px-3 py-1 text-gray-500 hover:text-primary"
          active-class="text-primary"
        >
          <UIcon name="i-lucide-shopping-cart" class="text-xl" />
          <span class="text-[10px] font-medium">Keranjang</span>
        </NuxtLink>
        <NuxtLink
          to="/pesanan"
          class="flex flex-col items-center gap-1 px-3 py-1 text-gray-500 hover:text-primary"
          active-class="text-primary"
        >
          <UIcon name="i-lucide-package" class="text-xl" />
          <span class="text-[10px] font-medium">Pesanan</span>
        </NuxtLink>
        <NuxtLink
          to="/profil"
          class="flex flex-col items-center gap-1 px-3 py-1 text-gray-500 hover:text-primary"
          active-class="text-primary"
        >
          <UIcon name="i-lucide-user" class="text-xl" />
          <span class="text-[10px] font-medium">Profil</span>
        </NuxtLink>
      </div>
    </nav>
  </UApp>
</template>
