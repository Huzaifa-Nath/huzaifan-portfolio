
<script setup>
import { ref, defineExpose, onMounted, onBeforeUnmount, defineProps } from 'vue'
import { useScrollContext } from '../composables/useScrollContext'

const props = defineProps({
  id: {
    type: String,
    required: true
  },
  overflowHidden: {
    type: Boolean,
    default: true
  },
  noPadding: { type: Boolean, default: false }

})

const sectionRef = ref(null);
const { registerSection, unregisterSection } = useScrollContext();

onMounted(() => registerSection(props.id, sectionRef.value));
onBeforeUnmount(() => unregisterSection(props.id));
defineExpose({ sectionRef });
</script>

<template>
   <section
   ref="sectionRef"
  :id="props.id"
  :class="[
    'w-full snap-start',
    props.overflowHidden && 'overflow-hidden',
    !props.noPadding && 'p-[3dvw]'
  ]"
>

  <slot></slot>
</section>

</template>
