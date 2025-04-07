<template>
  <component :is="currentComponent" />
</template>

<script setup>
import { ref, onMounted, onUnmounted, markRaw } from "vue";
import _Desktop from "@/components/Desktop.vue";
import _Mobil from "@/components/Mobil.vue";

const Desktop = markRaw(_Desktop)
const Mobil = markRaw(_Mobil)

const isMobile = ref(window.innerWidth < 768);
const currentComponent = ref(isMobile.value ? Mobil : Desktop);

const updateSize = () => {
  isMobile.value = window.innerWidth < 768;
  currentComponent.value = isMobile.value ? Mobil : Desktop;
};

onMounted(() => {
  window.addEventListener("resize", updateSize);
});

onUnmounted(() => {
  window.removeEventListener("resize", updateSize);
});
</script>
