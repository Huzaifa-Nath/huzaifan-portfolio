<script setup>
import { ref, onMounted } from 'vue';
import TextAnim from '../components/TextAnim.vue'
import FramedMainSection from '../layouts/FramedMainSection.vue';

const frameRef = ref(null);
const containerRef = ref(null);

onMounted(() => {
    containerRef.value = frameRef.value.sectionRef;
});
</script>

<template>
    <FramedMainSection ref="frameRef" id="home"  class="lg:h-screen min-h-[88vh] overflow-hidden">
        <div 
            class="h-full w-full bg-fit bg-cover bg-position-[center_40%]  rounded-[2rem] bg-[url('/backgrounds/mountains.png')] flex flex-col justify-center items-center text-center">
            <div
                class="text-[#fff] font-rubik uppercase text-[10dvw] xl:text-[13dvh]  leading-none flex flex-col justify-center items-center ">
             
                <p class="flex h-[8.4dvw] xl:h-[13dvh] overflow-hidden">
                    <span class="standard-text">I </span>
                    <TextAnim 
                        v-if="containerRef"
                        :texts="['Build', 'Develop', 'Impact', 'Change', 'Design']" 
                        :container="containerRef" 
                        :duration="2.5" 
                        :class="'text-[#de2e2e] -z-100'" 
                    />
                </p>
                <p class="flex h-[8.4dvw] xl:h-[12dvh] ">products</p>
                <p class="flex h-[8.4dvw] xl:h-[12dvh] ">that merge</p>
                <p class="flex h-[8.4dvw] xl:h-[12dvh] ">logic with </p>
                <p class="flex h-[8.4dvw] xl:h-[12dvh] ">creativity</p>

            </div>
        </div>
    </FramedMainSection>
</template>

