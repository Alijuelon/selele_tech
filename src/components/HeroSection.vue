<script setup>
import { ref, onMounted } from 'vue';

// Mengubah daftar proyek menjadi relevan dengan Hardware & PC Building
const projects = ref([
  // Bidang Hardware & Windows (Reza)
  { id: 1, title: 'Custom PC Build & Cable Management', category: 'Hardware Assembly', image: 'https://images.unsplash.com/photo-1587202372634-32705e3bf49c?auto=format&fit=crop&q=80&w=1200&h=800' },
  { id: 2, title: 'Laptop Optimization & Cleaning', category: 'Maintenance', image: 'https://images.unsplash.com/photo-1597872200969-2b65d56bd16b?auto=format&fit=crop&q=80&w=1200&h=800' },
  { id: 3, title: 'OS Reinstall & Troubleshooting', category: 'Windows System', image: 'https://images.unsplash.com/photo-1629654297299-c8506221ca97?auto=format&fit=crop&q=80&w=1200&h=800' },
  
  // Bidang Software & Web/Mobile (Ali)
  { id: 4, title: 'Enterprise Web & Mobile App', category: 'Software Development', image: 'https://images.unsplash.com/photo-1512941937669-90a1b58e7e9c?auto=format&fit=crop&q=80&w=1200&h=800' },
  
  // Bidang Jaringan & Keamanan (Ridho)
  { id: 5, title: 'Network Architecture & Security Audit', category: 'Cyber Security', image: 'https://images.unsplash.com/photo-1526374965328-7f61d4dc18c5?auto=format&fit=crop&q=80&w=1200&h=800' },
  { id: 6, title: 'Linux Server & System Hardening', category: 'Infrastructure', image: 'https://images.unsplash.com/photo-1629654291663-b91ad427698f?auto=format&fit=crop&q=80&w=1200&h=800' }
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
        <h1 class="text-5xl sm:text-6xl lg:text-7xl font-serif font-extrabold text-slate-900 dark:text-white leading-tight mb-6 text-justify">
          All Solusion<br />
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-emerald-400 italic">
            Performa Maksimal.
          </span>
        </h1>
        <p class="font-serif text-lg text-slate-600 dark:text-slate-400 mb-8 max-w-lg leading-relaxed text-justify tracking-wide">
          Pusat solusi IT terintegrasi untuk skala personal maupun enterprise. Mulai dari perakitan hardware, optimalisasi PC, dan pemeliharaan sistem Windows, hingga pengembangan website dan aplikasi mobile lintas platform berkinerja tinggi. Kami juga menghadirkan layanan arsitektur serta audit keamanan jaringan untuk memastikan seluruh infrastruktur digital Anda berjalan kencang, aman, dan tanpa kendala.
        </p>
        <a href="#operatives" class="inline-block px-8 py-4 glass-panel text-slate-900 dark:text-white font-bold rounded-lg transition-transform hover:scale-105 border-cyan-500/30 hover:border-cyan-400">
          Lihat Profil Teknisi
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