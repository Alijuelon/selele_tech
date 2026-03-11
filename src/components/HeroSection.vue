<script setup>
import { ref, onMounted } from 'vue';

const projects = ref([
  { id: 1, title: 'Server Room Deployment', category: 'Networking', image: 'https://picsum.photos/seed/server/1200/800' },
  { id: 2, title: 'Smart Agriculture IoT', category: 'IoT & Firmware', image: 'https://picsum.photos/seed/iot/1200/800' },
  { id: 3, title: 'Enterprise App Dashboard', category: 'Software Dev', image: 'https://picsum.photos/seed/dashboard/1200/800' }
]);

const activeSlide = ref(0);

onMounted(() => {
  setInterval(() => {
    activeSlide.value = (activeSlide.value + 1) % projects.value.length;
  }, 4000); // Ganti slide tiap 4 detik
});
</script>

<template>
  <section id="intro" class="relative pt-32 pb-20 sm:pt-40 sm:pb-32 overflow-hidden flex items-center min-h-[90vh]">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 w-full z-10 grid lg:grid-cols-2 gap-12 items-center">
      
      <div class="animate-fadeInUp opacity-0" style="animation-fill-mode: forwards;">
        <h1 class="text-5xl sm:text-6xl lg:text-7xl font-serif font-extrabold text-slate-900 dark:text-white leading-tight mb-6">
          Arsitektur <br />
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-emerald-400 italic">
            Digital Ekstrem.
          </span>
        </h1>
        <p class="text-lg text-slate-600 dark:text-slate-400 mb-8 max-w-lg leading-relaxed">
          SeleseTech Node. Hub operasional untuk komputasi performa tinggi, pengembangan sistem cerdas lintas platform, dan arsitektur jaringan korporat.
        </p>
        <a href="#operatives" class="inline-block px-8 py-4 glass-panel text-slate-900 dark:text-white font-bold rounded-lg transition-transform hover:scale-105 border-cyan-500/30 hover:border-cyan-400">
          Inisiasi Protokol
        </a>
      </div>

      <div class="relative h-[400px] w-full card-3d-wrap animate-fadeInUp delay-200 opacity-0" style="animation-fill-mode: forwards;">
        <div class="card-3d w-full h-full relative rounded-2xl overflow-hidden glass-panel p-2 shadow-2xl">
          <div v-for="(proj, index) in projects" :key="proj.id" 
               class="absolute inset-2 rounded-xl overflow-hidden transition-opacity duration-1000"
               :class="index === activeSlide ? 'opacity-100 z-10' : 'opacity-0 z-0'">
            <img :src="proj.image" alt="Project" class="object-cover w-full h-full scale-105 animate-float" />
            <div class="absolute bottom-4 left-4 right-4 glass-panel p-4 rounded-lg backdrop-blur-md">
              <span class="text-xs font-bold text-cyan-400 uppercase tracking-widest">{{ proj.category }}</span>
              <h3 class="text-xl font-serif font-bold text-white mt-1">{{ proj.title }}</h3>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>