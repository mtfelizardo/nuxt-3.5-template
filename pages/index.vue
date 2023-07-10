<template>
  <Container>
    <section>
      <h1 class="text-2xl text-gray-800 font-semibold mb-2">Getting Started</h1>
      <p>This is the first page of the template, the homepage. </p>
      <p>You can delete this page and start you project from here. Location: <strong>pages/index.vue</strong></p>
    </section>

    <section class="mt-6">
      <h2 class="text-xl text-gray-800 font-semibold mb-2"># About</h2>
      <p>All components are located in <strong>/components</strong>.</p>
      <p>They were created using tailwind but you can use SCSS in the scoped style as well.</p>
    </section>

    <section class="my-6">
      <h2 class="text-xl text-gray-800 font-semibold mb-2"># Components</h2>

      <div class="grid grid-cols-3 gap-4 mt-4">
        <div 
          class="bg-white rounded-md p-4 shadow-md"
          v-for="(component, index) in components" 
          :key="component.name + index"
        >
            <h3 class="text-green-500 text-xl font-semibold mb-2">{{ component.name }}</h3>
            <p class="mb-2 text-sm" v-html="component.description"></p>
            <button @click="toggleComponent(component)" :class="component.visible ? 'bg-red-500'  : 'bg-green-500' " class="text-white px-4 rounder-md min-w-[72px] pointer-events-auto">
              <span v-if="!component.visible">Show</span>
              <span v-else>Hide</span>
            </button>

            <div v-if="component.visible">
              <Teleport to="#__default">
                <component class="opacity-0 pointer-events-auto" :id="component.name" :is="component.component" />
              </Teleport>
            </div>
        </div>
      </div>
    </section>

  </Container>
</template>

<script setup>
  import gsap from 'gsap'
  const Isi = resolveComponent('Isi')

  const components = ref([
    {
      name: 'ISI',
      component: Isi,
      description: 'This is the initial components to render the ISI, it has a "sub-component" called <strong>ISIContent</strong> that is the one that renders the copy of the ISI.',
      visible: false,
    },
  ])

  const toggleComponent = (component) => {

    if (component.visible) {
      document.body.style.pointerEvents = ''

      gsap.to(`#${component.name}`, {
        opacity: 0,
        pointerEvents: 'auto',
        duration: .3,
        onComplete: () => {
          component.visible  = !component.visible 
        }
      })

      return
    }

    component.visible  = !component.visible 
    document.body.style.pointerEvents = 'none'

    setTimeout(()=> {
      gsap.to(`#${component.name}`, {
      opacity: 1,
      duration: 1
    })
    }, 100)
  }

 
</script>
