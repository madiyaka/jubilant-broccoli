<template>
  <div class="relative w-full min-h-screen overflow-hidden font-serif">
    <!-- 🎥 Видео на фоне -->
    <video
      autoplay
      muted
      loop
      playsinline
      class="fixed top-0 left-0 w-full h-full object-cover z-[-1]"
    >
      <source src="/assets/images/river-vials-dota-2-moewalls-com.mp4" type="video/mp4" />
    </video>

    <!-- ⬆️ Верхняя панель -->
    <header class="flex w-full items-center justify-between bg-black bg-opacity-80 text-white border-b border-gray-800 px-6 py-4 max-sm:flex-col max-sm:items-start">
      <!-- Логотип -->
      <div class="flex items-center w-50 h-16">
        <img src="/assets/images/logo.png" alt="Home" class="w-50 h-16" />
      </div>

      <!-- Навигация -->
      <nav class="flex items-center justify-center gap-10 text-xl font-semibold max-sm:flex-col max-sm:items-start">
        <NuxtLink to="/" class="p-2 hover:text-yellow-500">Home</NuxtLink>
        
        <!-- Выпадающее меню Labs -->
        <div class="relative group">
          <span class="p-2 hover:text-yellow-500 cursor-pointer">Labs</span>
          <div class="absolute hidden group-hover:flex flex-col top-full bg-black bg-opacity-90 text-white w-56 text-center font-semibold z-20">
            <NuxtLink v-for="lab in labs" :key="lab.path" :to="lab.path" class="p-2 hover:text-yellow-500">
              {{ lab.name }}
            </NuxtLink>
          </div>
        </div>

        <NuxtLink to="/login" class="p-2 hover:text-yellow-500">LogIn</NuxtLink>
        <NuxtLink to="/logout" class="p-2 hover:text-yellow-500">LogOut</NuxtLink>
      </nav>
    </header>

    <!-- 📄 Контент -->
    <main class="relative z-10 bg-black bg-opacity-60 text-white min-h-screen px-6 py-12">
      <slot></slot>
    </main>

    <!-- ⬇️ Футер -->
    <footer class="relative z-10 bg-black bg-opacity-80 text-white py-4 text-center">
      <div class="flex justify-center gap-4 items-center">
        <a v-for="social in socialLinks" :key="social.name" :href="social.url" :aria-label="social.name" target="_blank" rel="noopener noreferrer">
          <img :src="social.icon" :alt="social.name" class="w-16 h-16" loading="lazy" />
        </a>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { useHead } from "#app"

const labs = [
  { name: 'Lab3', path: '/Lab3' },
  { name: 'Lab4', path: '/Lab4' },
  { name: 'Lab5', path: '/Lab5' },
  { name: 'Lab6', path: '/Lab6' },
]

const socialLinks = [
  { name: 'YouTube', url: 'http://www.youtube.com/', icon: '/images/youtube.png' },
  { name: 'GitHub', url: 'http://github.com/', icon: '/images/github.png' },
  { name: 'Facebook', url: 'http://www.facebook.com', icon: '/images/facebook.png' },
]

useHead({
  script: [
    {
      async: true,
      src: 'https://www.googletagmanager.com/gtag/js?id=G-FKZWBZW3GH',
    },
    {
      innerHTML: `
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', 'G-FKZWBZW3GH');
      `,
      type: 'text/javascript',
    },
  ],
  __dangerouslyDisableSanityzersByTagID: {
    gtag: ['innerHTML'],
  },
})
</script>

<style scoped>
.group:hover .group-hover\:flex {
  display: flex;
}
.group-hover\:flex {
  display: none;
}
</style>
