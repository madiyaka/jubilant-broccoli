<template>
   <header class="flex flex-row w-full items-center relative bg-red-800 text-white px-4 border-b-2 border-red-400 max-sm:justify-between max-sm:relative">
  <div class="basis-1/4 items-center justify-start px-8 min-w-40 max-sm:basis-auto">
    <img src="/assets/images/home.png" class="w-16 h-16 bg-transparent">
  </div>
  
  <div class="basis-1/4 max-sm:basis-auto">

  </div>

  <nav :class= "{'basis-1/2 flex items-center justify-end px-6 gap-2': !burger || burger,
    'max-sm:flex-col max-sm:bg-red-600 max-sm:basis-auto max-sm:absolute max-sm:top-full max-sm:w-full max-sm:justify-center': burger,
    'max-sm:hidden': !burger}">
      <NuxtLink to="/" class="my-auto p-2 hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:border-b-2 max-sm:border-black max-sm:text-center">Home</NuxtLink>
      <div class="my-auto p-2 hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:text-center max-sm:px-0 max-sm:pb-0" @click= "switch_submenu">Labs
        <div class="flex flex-col absolute top-full bg-white text-black w-56 text-center max-sm:relative max-sm:w-full" v-show = "submenu">
          <NuxtLink to="/Lab3" class="my-auto p-2 bg-red-600 text-white border-b-2 border-black hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:bg-red-500 max-sm:border-t-2 max-sm:text-center">Lab3</NuxtLink>
          <NuxtLink to="/Lab4" class="my-auto p-2 bg-red-600 text-white border-b-2 border-black hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:bg-red-500 max-sm:text-center">Lab4</NuxtLink>
          <NuxtLink to="/Lab5" class="my-auto p-2 bg-red-600 text-white border-b-2 border-black hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:bg-red-500 max-sm:text-center">Lab5</NuxtLink>
          <NuxtLink to="/Lab6" class="my-auto p-2 bg-red-600 text-white border-b-2 border-black hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:bg-red-500 max-sm:border-black max-sm:text-center">Lab6</NuxtLink>
        </div>
      </div>
      <NuxtLink to="/login" :class= "{'my-auto p-2 hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:border-b-2 max-sm:border-black max-sm:text-center': submenu,
      'my-auto p-2 hover:bg-yellow-500 hover:text-white max-sm:w-full max-sm:border-b-2 max-sm:border-t-2 max-sm:border-black max-sm:text-center':!submenu}">LogIn</NuxtLink>
      <NuxtLink to="/logout" class="my-auto p-2 hover:bg-yellow-500 hover:text-black max-sm:w-full max-sm:border-b-2 max-sm:border-black max-sm:text-center">LogOut</NuxtLink>
  </nav>

  <div v-if= "!burger" @click="switch_burger" class="max-sm:flex max-sm:flex-col max-sm:my-1 max-sm:justify-between max-sm:items-center max-sm:w-8 max-sm:h-6">
    <span class="h-[3px] w-full bg-white"></span>
    <span class="h-[3px] w-full bg-white"></span>
    <span class="h-[3px] w-full bg-white"></span>
  </div>

  <div v-else class="max-sm:flex max-sm:flex-col max-sm:mr-8 max-sm:justify-between max-sm:items-center max-sm:w-8 max-sm:h-6" @click="switch_burger">
    <span class="h-[3px] w-full bg-white rotate-[45deg] relative top-[9px]"></span>
    <span class="h-[3px] w-full bg-white opacity-0"></span>
    <span class="h-[3px] w-full bg-white relative bottom-3 rotate-[-45deg]"></span>
  </div>
</header>


    <main class="p-5 flex  bg-red-200 h-screen">
        <slot />
    </main>

    <footer class="flex flex-row w-full bg-red-800 border-t-2 border-black items-center justify-center px-4 py-2 gap-4">
        <a href="http://www.youtube.com/"><img src="/assets/images/youtube.png" class="w-16 h-16"></a>
        <a href="http://github.com/"><img src="/assets/images/github.png" class="w-16  h-16"></a>
        <a href="http://www.facebook.com"><img src="/assets/images/facebook.png" class="w-16 h-16 bg-transparent"></a>  
    </footer>
</template>

<script setup lang="ts">
    import { useHead } from "#app"
    import {ref} from "vue"

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
    });

    const burger = ref<boolean>(false)
    const submenu = ref<boolean>(false)

    const switch_burger = ()=> {burger.value = !burger.value}
    const switch_submenu = ()=> {submenu.value = !submenu.value}
</script>



