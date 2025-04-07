<template>
  <aside class="h-screen w-full flex flex-col items-center pt-16 font-deca x-12">
    <ProfileHeader />
    <button
      v-for="(item, index) in sections"
      :key="index"
      @click="changeSlide(index)"
      class="w-[244px] p-3 m-1 flex items-center gap-2 transition text-xs cursor-pointer font-medium border border-gray-200"
    >
      <div class="mx-3">
        <component :is="item.icon" :size="20"  class="hover:text-white" />
      </div>
      {{ item.name }}
    </button>
  </aside>
</template>

<script setup>
import ProfileHeader from './ProfileHeader.vue';

defineProps(["sections", "changeSlide"]);
</script>

<style></style>