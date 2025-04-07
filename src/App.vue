<template>
  <component :is="isMobile ? MobileComponent : DesktopComponent" />
</template>

<script setup>
import { markRaw } from "vue";
import Desktop from "./components/Desktop.vue";
import Mobile from "./components/Mobile.vue";

const DesktopComponent = markRaw(Desktop);
const MobileComponent = markRaw(Mobile);
</script>
