<script setup>
import { ref } from 'vue';

const catalogs = ref([
  {
    title: 'Hardware & OS Integration',
    category: 'Node: Hardware',
    image: 'https://picsum.photos/seed/pc/800/1000',
    shortDesc: 'Rakit PC Custom, Perawatan Bare-Metal, dan Hardening OS.',
    fullDesc: 'Layanan fisik mencakup perakitan PC High-End untuk kebutuhan workstation, rendering 3D, gaming, hingga server korporat. Kami menjamin manajemen kabel presisi tingkat militer. Kami juga menangani pembersihan debu level komponen mikron, penggantian thermal paste premium (liquid metal), instalasi ulang OS bebas bloatware, hingga penyelamatan data kritis dari hard drive yang terinfeksi ransomware.',
    tools: ['Thermal Grizzly', 'Windows Server', 'Linux Kernel', 'Data Recovery Tool', 'Custom Liquid Cooling']
  },
  {
    title: 'App Ecosystem & IoT',
    category: 'Node: Software',
    image: 'https://picsum.photos/seed/code/800/1000',
    shortDesc: 'Pembuatan Web Enterprise (Laravel), App Mobile (Flutter) & Node IoT.',
    fullDesc: 'Kami membangun arsitektur perangkat lunak dari hulu ke hilir. Backend API berkinerja tinggi menggunakan framework Laravel untuk menangani puluhan ribu request konkuren, dipadukan dengan aplikasi mobile lintas platform berbasis Flutter yang smooth (60fps). Di ranah interaksi fisik, kami membuat prototipe IoT cerdas menggunakan mikrokontroler ESP32/Arduino untuk mengotomatisasi proses bisnis Anda, seperti smart farming, monitoring suhu, atau smart home terpadu.',
    tools: ['Flutter / Dart', 'Laravel 10 / PHP 8', 'ESP32 / Arduino', 'Firebase / Supabase', 'RESTful API']
  },
  {
    title: 'Network & Cyber Security',
    category: 'Node: Network',
    image: 'https://picsum.photos/seed/network/800/1000',
    shortDesc: 'Infrastruktur Fiber, Mikrotik/Cisco, dan Hardening Server.',
    fullDesc: 'Membangun "jalan tol" digital berkecepatan tinggi tanpa bottleneck untuk instansi Anda. Layanan ini mencakup penarikan kabel LAN/Fiber Optic skala gedung secara terstruktur. Konfigurasi router tingkat lanjut (MikroTik/Cisco) untuk load balancing multi-ISP dan pembagian bandwidth yang adil (QoS). Di sisi keamanan siber, kami melakukan setup Firewall ketat, enkripsi VPN untuk remote working, serta hardening pada Web Server untuk mencegah serangan DDoS dan injeksi kode.',
    tools: ['MikroTik RouterOS', 'Cisco IOS Switching', 'Fiber Splicing', 'Kali Linux (Pentest)', 'IPsec VPN']
  }
]);

const activeService = ref(null);

const openModal = (srv) => { 
  activeService.value = srv; 
  document.body.style.overflow = 'hidden'; 
};

const closeModal = () => { 
  activeService.value = null; 
  document.body.style.overflow = 'auto'; 
};
</script>

<template>
  <section id="stack" class="py-24 relative z-10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
      <div class="text-center mb-20 animate-fadeInUp">
        <h2 class="text-4xl sm:text-5xl font-serif font-bold text-slate-900 dark:text-white transition-colors duration-300">Solution Stack.</h2>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-10">
        <div v-for="(cat, idx) in catalogs" :key="idx" @click="openModal(cat)"
             class="card-3d-wrap cursor-none animate-fadeInUp opacity-0" :class="`delay-${(idx+1)*100}`" style="animation-fill-mode: forwards;">
          
          <div class="card-3d relative rounded-2xl overflow-hidden glass-panel h-[420px] group border border-slate-200 dark:border-slate-800 transition-all hover:border-cyan-500/50">
            <img :src="cat.image" class="absolute inset-0 w-full h-full object-cover opacity-60 dark:opacity-40 group-hover:opacity-100 group-hover:scale-110 transition-all duration-700 pointer-events-none" />
            
            <div class="absolute inset-0 bg-gradient-to-t from-slate-900 via-slate-900/80 to-slate-900/20 dark:from-slate-950 dark:via-slate-950/80 dark:to-transparent"></div>
            
            <div class="absolute inset-0 bg-cyan-500/10 opacity-0 group-hover:opacity-100 transition-opacity duration-500 mix-blend-overlay"></div>

            <div class="absolute bottom-0 left-0 right-0 p-8 flex flex-col h-full justify-end z-10">
              <span class="text-xs font-bold text-cyan-400 uppercase tracking-widest mb-3 transform translate-y-4 group-hover:translate-y-0 transition-transform duration-500">{{ cat.category }}</span>
              <h3 class="text-2xl font-serif font-bold text-white mb-3 tracking-tight transform translate-y-4 group-hover:translate-y-0 transition-transform duration-500 delay-75">{{ cat.title }}</h3>
              <p class="text-slate-300 text-sm mb-6 leading-relaxed opacity-0 group-hover:opacity-100 transform translate-y-4 group-hover:translate-y-0 transition-all duration-500 delay-100 line-clamp-2">{{ cat.shortDesc }}</p>
              
              <div class="inline-flex items-center justify-center bg-white/10 backdrop-blur-md border border-white/20 text-white text-xs font-bold px-5 py-2.5 rounded-full group-hover:bg-cyan-500 group-hover:border-cyan-400 transition-colors shadow-lg opacity-0 group-hover:opacity-100 transform translate-y-4 group-hover:translate-y-0 duration-500 delay-150 self-start">
                Ekstrak Detail <span class="ml-2 text-sm">⎋</span>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>

    <Teleport to="body">
      <Transition name="backdrop">
          <div v-if="activeService" class="fixed inset-0 z-[99998] bg-slate-950/90 backdrop-blur-md cursor-none" @click="closeModal"></div>
      </Transition>

      <Transition name="flip">
          <div v-if="activeService" class="fixed inset-0 z-[99999] flex items-center justify-center p-4 sm:p-6 lg:p-10 cursor-none overscroll-contain" @click="closeModal">
              
              <div class="relative w-full max-w-6xl max-h-[90dvh] bg-slate-100 dark:bg-slate-950 rounded-2xl shadow-2xl overflow-y-auto border border-slate-200 dark:border-cyan-900/50 custom-scrollbar flex flex-col md:flex-row shadow-cyan-500/5 cursor-none" @click.stop>
                  
                  <button @click="closeModal" class="absolute top-5 right-5 z-50 w-12 h-12 rounded-full glass-panel bg-slate-900/80 border border-slate-700 text-white flex items-center justify-center hover:bg-cyan-500 hover:scale-110 transition-all text-2xl font-black shadow-lg">✕</button>
                  
                  <div class="md:w-[40%] bg-slate-200 dark:bg-slate-900 md:sticky top-0 h-72 md:h-auto border-b md:border-b-0 md:border-r border-slate-300 dark:border-slate-800 relative overflow-hidden group">
                    <div class="absolute inset-0 bg-gradient-to-t from-slate-200 dark:from-slate-900 via-transparent to-transparent z-10"></div>
                    <div class="absolute top-6 left-6 z-20 glass-panel px-4 py-2 rounded-lg border border-cyan-500/30 text-cyan-400 font-bold text-xs tracking-widest uppercase flex items-center gap-2">
                      <span class="w-2 h-2 rounded-full bg-cyan-400 animate-pulse"></span>
                      {{ activeService.category }}
                    </div>
                    <img :src="activeService.image" class="object-cover w-full h-full opacity-90 dark:opacity-70 group-hover:scale-105 transition-transform duration-1000" />
                  </div>

                  <div class="p-8 md:p-14 md:w-[60%] text-slate-800 dark:text-slate-300 flex flex-col justify-center">
                    
                    <h3 class="text-4xl sm:text-5xl font-serif font-bold mb-8 text-slate-950 dark:text-white leading-tight tracking-tight mt-4 md:mt-0">{{ activeService.title }}</h3>
                    
                    <p class="text-base sm:text-lg leading-relaxed mb-12 text-slate-700 dark:text-slate-400 font-medium border-l-4 border-cyan-500 pl-6 bg-slate-200/50 dark:bg-slate-900/50 py-4 rounded-r-xl">
                      {{ activeService.fullDesc }}
                    </p>
                    
                    <div>
                      <h4 class="font-serif font-bold text-2xl mb-6 text-slate-900 dark:text-white flex items-center gap-3">
                        <svg class="w-6 h-6 text-cyan-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path></svg>
                        Technical Tools & Frameworks
                      </h4>
                      <div class="flex flex-wrap gap-3">
                        <span v-for="tool in activeService.tools" :key="tool" class="px-5 py-2.5 bg-white dark:bg-slate-800 border border-slate-300 dark:border-slate-700 rounded-lg text-sm text-slate-800 dark:text-cyan-300 font-bold shadow-sm hover:border-cyan-500 dark:hover:border-cyan-500 transition-colors cursor-none">
                          {{ tool }}
                        </span>
                      </div>
                    </div>

                    <div class="mt-14 pt-8 border-t border-slate-300 dark:border-slate-800">
                      <a href="#initialize" @click="closeModal" class="inline-flex items-center gap-3 bg-cyan-600 text-white px-8 py-4 rounded-lg font-bold hover:bg-cyan-500 transition-all hover:scale-105 shadow-[0_0_20px_rgba(6,182,212,0.3)] cursor-none">
                        Konsultasi Layanan Ini <span class="text-xl">→</span>
                      </a>
                    </div>

                  </div>
              </div>
          </div>
      </Transition>
    </Teleport>
  </section>
</template>

<style scoped>
/* Scrollbar khusus untuk modal */
.custom-scrollbar::-webkit-scrollbar { width: 5px; }
.custom-scrollbar::-webkit-scrollbar-track { background: rgba(10, 15, 28, 0.8); border-radius: 10px; }
.custom-scrollbar::-webkit-scrollbar-thumb { background: #06b6d4; border-radius: 10px; }
.custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #22d3ee; }
</style>