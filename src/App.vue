<script setup>
import ScrollBar from './components/Scrollbar.vue'
import LiquidNavbar from './components/LiquidNavbar.vue'
import Home from './views/Home.vue'
import AboutMe from './views/AboutMe.vue'
import AboutMeMobile from './views/AboutMeMobile.vue'
import Projects from './views/Projects.vue'
import Contact from './views/Contact.vue'
import { provideScrollContext } from './composables/useScrollContext'
import { useCursorContext } from './composables/useCursorContext'
import { useWindowContext } from './composables/useWindowContext'
import { ref, onMounted } from 'vue'
import { AnimatedComponent } from './services/AnimatedComponent'

const { containerRef, contentRef } = provideScrollContext()
const { setPositions } = useCursorContext()
const { resetWidth, md } = useWindowContext()

const component = ref()
const windowComponent = ref()


onMounted(() => {
  component.value = new AnimatedComponent()
  component.value.tick = (e) => {
    if (e instanceof MouseEvent) setPositions(e.clientX, e.clientY)
  }
  component.value.addAnimationTrigger(window, "mousemove")

  windowComponent.value = new AnimatedComponent()
  windowComponent.value.tick = resetWidth
  windowComponent.value.addAnimationTrigger(window, "resize")
})
</script>


<template>  
  <ScrollBar />

  <div
  ref="containerRef"
  class="overflow-auto h-screen flex flex-col items-center font-ledger custom-scroll-container"
>
    <LiquidNavbar />

    <div ref="contentRef" class="w-full flex flex-col">
      <Home />
      <AboutMe v-if="md" />
      <AboutMeMobile v-else />
      <Projects :images="images"/>
      <Contact />
    </div>
  </div>
</template>
