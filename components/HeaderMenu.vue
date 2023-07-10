<template>
  <nav class="py-4 px-8 bg-black flex justify-between items-center">
    <NuxtLink to="/" class="w-[140px] block" >
      <img src="~/assets/images/envivent_logo.png" alt="Envivent">
    </NuxtLink>

    <div class="flex items-center gap-5">
      <div v-for="(url, index) in urls" :key="url.text + index">
        <NuxtLink
          :to="url.url"
          class="text-white uppercase text-sm font-bold tracking-wider hover:text-green-400"
        >
          {{ url.text }}
        </NuxtLink>
      </div>
    </div>
  </nav>
</template>

<script setup>

 const urls = [
  {
    text: 'components',
    url: '/components'
  },
  {
    text: 'demos',
    url: '/demos'
  },
 ]
</script>
