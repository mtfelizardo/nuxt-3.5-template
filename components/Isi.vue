<template>
  <div class="bg-white">
    <div v-if="isShowingFloating" ref="floatingIsiRef" class="bg-white fixed top-[calc(100%-160px)]">
      <button class="absolute right-2 top-2" @click="goToFixed">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M7.41 8.58L12 13.17l4.59-4.59L18 10l-6 6l-6-6l1.41-1.42Z"/></svg>
      </button>
      <IsiContent />
    </div>

    <div class="mt-[400px]">
      <IsiContent ref="fixedIsiRef"/>
    </div>
  </div>
</template>

<script setup>
  import gsap from 'gsap'
  import { ScrollTrigger } from "gsap/ScrollTrigger";

  const isShowingFloating = ref(true)
  const floatingIsiRef = ref(null)
  const fixedIsiRef = ref(null)
  gsap.registerPlugin(ScrollTrigger);

  const goToFixed = () => {
    fixedIsiRef.value.$el.scrollIntoView({behavior: 'smooth'})
  }

  onMounted(()=> {
    gsap.to(fixedIsiRef.value, {
      scrollTrigger: {
        trigger: fixedIsiRef.value.$el,
        start: "top bottom-=100",
        end: "bottom top+=100",
        onEnter: () => {
          gsap.to(floatingIsiRef.value, {
            opacity: 0,
            duration: 0.5
          })
        },
        onLeaveBack: () => {
          gsap.to(floatingIsiRef.value, {
            opacity: 1,
            duration: 0.5
          })
        }
      }, 
    })
  })

</script>
