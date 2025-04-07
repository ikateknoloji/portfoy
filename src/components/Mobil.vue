<template>
  <div class="relative overflow-hidden">
    <!-- Açılır içerik paneli -->
    <main
      ref="panel"
      class="fixed bottom-0 left-0 right-0 top-12 z-[10] rounded-t-2xl overflow-y-auto
       transition-transform duration-500
       shadow-[0px_-3px_8px_rgba(0,0,0,0.3)]
       font-deca bg-white/90 backdrop-blur-xs rounded-t-4xl py-8 px-4 m-1"
       :class="activeSection ? 'translate-y-0' : 'translate-y-full'"
      @touchstart="startTouch"
      @touchmove="handleTouchMove"
    >
      <button @click="closeSection" class="fixed top-4 right-4 text-2xl font-bold z-10 hover:text-gray-900">
        <svg class="border-2 border-gray-100 " width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M4 22.32L10.3467 16L4 9.68L9.68 4L16 10.3467L22.32 4L28 9.68L21.6533 16L28 22.32L22.32 28L16 21.6533L9.68 28L4 22.32ZM16 17.88L22.32 24.2133L24.2133 22.32L17.88 16L24.2133 9.68L22.32 7.78667L16 14.12L9.68 7.78667L7.78667 9.68L14.12 16L7.78667 22.32L9.68 24.2133L16 17.88Z" fill="#111111"/>
        </svg>
      </button>
      <component :is="activeSection?.component" v-if="activeSection" />
    </main>

    <Sidebar :sections="sections" :changeSlide="openSection" />
  </div>
</template>

<script setup>
import Sidebar from "@/components/mobilebar/Sidebar.vue";
import { ref, markRaw } from "vue";
import Home from "@/components/mobil/Home.vue";
import AboutMe from "@/components/mobil/AboutMe.vue";
import Experience from "@/components/mobil/Experience.vue";
import Education from "@/components/mobil/Education.vue";
import Partners from "@/components/mobil/Partners.vue";
import Collaboration from "@/components/mobil/Collaboration.vue";
import gsap from "gsap";
import { User, Briefcase, GraduationCap, Handshake, Mail, House } from 'lucide-vue-next';

const sections = [
  { name: "Anasayfa", component: markRaw(Home), icon: House },
  { name: "Benim Hakkımda", component: markRaw(AboutMe), icon: User },
  { name: "Deneyimlerim", component: markRaw(Experience), icon: Briefcase },
  { name: "Eğitim Hayatım", component: markRaw(Education), icon: GraduationCap },
  { name: "İş Birliklerimiz", component: markRaw(Partners), icon: Handshake },
  { name: "İş Birliği", component: markRaw(Collaboration), icon: Mail },
];

const activeSection = ref(null);
const startY = ref(0);
const panel = ref(null);

const openSection = (index) => {
  activeSection.value = sections[index];

  // Önce paneli görünür yapalım
  gsap.set(panel.value, { y: "100%", opacity: 0 });

  // Sonra yukarı hareket ettirelim
  gsap.to(panel.value, {
    y: "0%",
    opacity: 1,
    duration: 0.5,
    ease: "power2.out"
  });
};

const closeSection = () => {
  gsap.to(panel.value, {
    y: "100%",
    opacity: .8,
    duration: 0.5,
    ease: "power2.out",
    onComplete: () => {
      activeSection.value = null;
    }
  });
};

const startTouch = (event) => {
  startY.value = event.touches[0].clientY;
};

const handleTouchMove = (event) => {
  const currentY = event.touches[0].clientY;
  const deltaY = currentY - startY.value;

  // Eğer içerik en üstteyse ve aşağı kaydırma hareketi gerçekleşiyorsa kapat
  if (deltaY > 50 && panel.value.scrollTop === 0) {
    closeSection();
  }
};
</script>
