<script setup>
import { onMounted, ref } from "vue";
import FramedMainSection from '../layouts/FramedMainSection.vue'
import projects from '../data/projects.json'
const mounted = ref(false);

onMounted(() => {
    setTimeout(() => {
        mounted.value = true;
    }, 100);
});
</script>



<template>
    <FramedMainSection id="projects" :noPadding="true" :overflowHidden="false">

        <main class="framed-wrapper">

            <div class="p-[3dvw] relative h-full cursor-pointer max-w-full w-full mx-auto">

                <a :href="project.url" target="_blank" rel="noopener noreferrer" v-for="(project, index) in projects"
                    :key="index" class="sticky w-full flex items-center justify-center mb-4"
                    :style="{ top: `${80 + (index * 40)}px` }">
                    <div class="project-card reveal-up w-full  rounded-[2rem] overflow-hidden"
                        :class="{ 'active': mounted }">
                        <div class="card-inner group " :style="{ backgroundImage: `url(${project.background})` }">
                            <div class="overlay transition-colors duration-700"></div>

                            <!-- Content -->
                            <div class="relative  z-10 text-center -">

                                <h2 class="font-rubik text-2xl  md:text-8xl text-white leading-tight">
                                    {{ project.title }}
                                </h2>
                                <p
                                    class="font-serif text-sm md:text-2xl p-5 text-white leading-relaxed  lg:max-w-3xl pt-10">
                                    {{ project.description }}
                                </p>
                            </div>


                        </div>
                    </div>
                </a>
            </div>
        </main>

    </FramedMainSection>
</template>


<style scoped>
body {
    background-color: var(--frame-color);
}

.framed-wrapper {
    min-height: 100vh;
    background-color: var(--frame-color);
}

.project-card {
    transition: transform 0.8s cubic-bezier(0.2, 1, 0.36, 1);
}

.card-inner {
    background-size: cover;
    background-position: center;
    height: 80vh;
    width: 100%;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;

}

.overlay {
    background: linear-gradient(to bottom,
            rgba(0, 0, 0, 0.2),
            rgba(0, 0, 0, 0.5));
    position: absolute;
    inset: 0;
}

/* Reveal Animation */
.reveal-up {
    opacity: 0;
    transform: translateY(40px);
    transition: all 1s cubic-bezier(0.22, 1, 0.36, 1);
}

.reveal-up.active {
    opacity: 1;
    transform: translateY(0);
}
</style>
