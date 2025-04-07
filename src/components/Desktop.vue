<template>
  <div class="grid grid-cols-12 min-h-screen overflow-hidden">
    <!-- Sidebar -->
    <Sidebar :sections="sections" :changeSlide="changeSlide" />

    <!-- Sağ Panel -->
    <main class="col-span-9 relative overflow-hidden">
      <div ref="carouselContainer" class="relative flex h-full" :style="{ width: `${(sections.length +1) * 900}px` }">
        <div
          v-for="(section, index) in sections"
          :key="index"
          @click="changeSlide(index)"
          class="w-[750px] h-full flex items-center justify-center text-xl cursor-pointer"
        >
          <component :is="section.component" />
        </div>
        <div  class="w-[750px] h-full flex items-center justify-center text-xl cursor-pointer"
        >
        <div class="relative flex flex-col justify-center  w-full h-screen bg-cover bg-center bg-no-repeat p-16
        " style="background-image: url('/final.jpg');">
        </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import Sidebar from "@/components/sidebar/Sidebar.vue";
import { ref, markRaw } from "vue";
import { gsap } from "gsap";
import Home from "@/components/Home.vue";
import AboutMe from "@/components/AboutMe.vue";
import Experience from "@/components/Experience.vue";
import Education from "@/components/Education.vue";
import Partners from "@/components/Partners.vue";
import Collaboration from "@/components/Collaboration.vue";

import { User, Briefcase, GraduationCap, Handshake, Mail, House } from 'lucide-vue-next';

const sections = ref([
  { name: "Anasayfa", component: markRaw(Home), icon: House },
  { name: "Benim Hakkımda", component: markRaw(AboutMe), icon: User },
  { name: "Deneyimlerim", component: markRaw(Experience), icon: Briefcase },
  { name: "Eğitim Hayatım", component: markRaw(Education), icon: GraduationCap },
  { name: "İş Birliklerimiz", component: markRaw(Partners), icon: Handshake },
  { name: "İş Birliği", component: markRaw(Collaboration), icon: Mail },
]);

const carouselContainer = ref(null);

const changeSlide = (index) => {
  gsap.to(carouselContainer.value, {
    x: `-${index * 750}px`,
    duration: 1,
    ease: "power2.out",
  });
};
</script>
