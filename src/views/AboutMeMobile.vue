<script setup>
import { ref, onMounted, watch } from 'vue'
import FramedMainSection from '../layouts/FramedMainSection.vue'
import stories from '../data/about-me.json'

const typedText = ref('')
const currentStoryIndex = ref(0)
const isTyping = ref(false)
let typingTimeout = null

const typeWriter = (text) => {
  if (typingTimeout) clearTimeout(typingTimeout)

  typedText.value = ''
  isTyping.value = true
  let i = 0

  const type = () => {
    if (i < text.length) {
      typedText.value += text[i++]
      typingTimeout = setTimeout(type, 18)
    } else {
      isTyping.value = false
    }
  }

  type()
}

watch(currentStoryIndex, (index) => {
  typeWriter(stories[index].description)
})

const selectStory = (index) => {
  if (isTyping.value) return
  currentStoryIndex.value = index
}

onMounted(() => {
  typeWriter(stories[0].description)
})
</script>



<template>
  <FramedMainSection
    id="about-me"
    class="text-[#58a6ff] font-mono"
  >
    <div class="border border-[#30363d] min-h-[88vh] rounded-3xl bg-[#0d1117] px-6 py-5">
      
      <!-- Header -->
      <div class="border border-[#30363d] rounded-3xl bg-[#161b22] p-2 flex gap-2 items-center mb-6">
        <div class="w-3 h-3 rounded-full bg-[#ff5f56]"></div>
        <div class="w-3 h-3 rounded-full bg-[#ffbd2e]"></div>
        <div class="w-3 h-3 rounded-full bg-[#27c93f]"></div>
        <span class="ml-2 text-xs text-[#8b949e]">
          nathh@portfolio:~/about-me
        </span>
      </div>

      <!-- Navigation -->
      <div class="mb-8 space-y-2">
        <div
          v-for="(story, i) in stories"
          :key="i"
          class="cursor-pointer transition-all duration-200"
          :class="currentStoryIndex === i
            ? 'text-[#58a6ff] font-bold'
            : 'text-[#8b949e] hover:text-[#c9d1d9]'"
          @click="selectStory(i)"
        >
          <span class="mr-2">$</span>
          <span class="underline decoration-dotted">
            cd ./{{ story.when }}
          </span>
          <span
            v-if="currentStoryIndex === i"
            class="ml-2 text-xs text-[#7ee787]"
          >
            &lt;&lt; HEAD
          </span>
        </div>
      </div>

      <!-- Content -->
      <div class="border-t border-[#30363d] pt-8">

        <!-- Image + Meta -->
        <div class="flex md:flex-row gap-8 items-center mb-8">

          <div class="md:w-1/3 aspect-square">
            <img
              :src="stories[currentStoryIndex].image"
              class="w-full h-full object-contain rounded-2xl "
            />
          </div>

          <div class="text-center">
            <h2 class="text-xl text-[#c9d1d9] font-bold">
              Time: "{{ stories[currentStoryIndex].when }}"
            </h2>
            <h3 class="text-base pt-2 text-[#8b949e]">
              Role: "{{ stories[currentStoryIndex].from }}"
            </h3>
          </div>

        </div>

        <!-- Typed Text -->
        <div class="text-[#c9d1d9] leading-relaxed text-sm tracking-wide ">
          <span class="text-[#ff7b72]">></span>
          {{ typedText }}
          <span class="animate-pulse">_</span>
        </div>

      </div>
    </div>
  </FramedMainSection>
</template>
