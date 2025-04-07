<template>
  <aside class="col-span-3 flex flex-col items-center justify-center font-deca shadow-2xl z-10">
    <ProfileHeader />
    <button
      v-for="(item, index) in sections"
      :key="index"
      @click="changeSlide(index)"
      class="w-[356px] p-3 m-2 flex items-center gap-2 transition text-sm cursor-pointer font-light border border-gray-100
      hover:border-gray-200 hover:bg-slate-950 hover:text-white transition-colors duration-300"
    >
      <div class="mx-3">
        <component :is="item.icon" :size="20"  class="hover:text-white" />
      </div>
      {{ item.name }}
    </button>
    <SocialLinks />
  </aside>
</template>

<script setup>
import ProfileHeader from './ProfileHeader.vue';
import SocialLinks from './SocialLinks.vue';

defineProps(["sections", "changeSlide"]);
</script>

<style></style>