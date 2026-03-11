<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import HeroSection from './components/HeroSection.vue';
import TeamCards from './components/TeamCards.vue';
import ServiceCatalog from './components/ServiceCatalog.vue';

// --- KURSOR & SHATTER LOGIC ---
const mouseX = ref(0);
const mouseY = ref(0);
const isClicking = ref(false);
const shatters = ref([]);
let shatterId = 0;

const updateMouse = (e) => {
  mouseX.value = e.clientX;
  mouseY.value = e.clientY;
};

const handleMouseDown = () => isClicking.value = true;
const handleMouseUp = () => isClicking.value = false;

const handleGlobalClick = (e) => {
  if (window.innerWidth >= 1024) {
    const id = shatterId++;
    shatters.value.push({ id, x: e.clientX, y: e.clientY });
    setTimeout(() => {
      shatters.value = shatters.value.filter(s => s.id !== id);
    }, 600); // Disesuaikan dengan durasi animasi CSS
  }
};

onMounted(() => {
  window.addEventListener('mousemove', updateMouse);
  window.addEventListener('mousedown', handleMouseDown);
  window.addEventListener('mouseup', handleMouseUp);
  window.addEventListener('click', handleGlobalClick);
  document.documentElement.classList.add('dark');
});

onUnmounted(() => {
  window.removeEventListener('mousemove', updateMouse);
  window.removeEventListener('mousedown', handleMouseDown);
  window.removeEventListener('mouseup', handleMouseUp);
  window.removeEventListener('click', handleGlobalClick);
});

// --- THEME & SMOOTH NAVIGATION LOGIC ---
const isDark = ref(true);
const isMobileMenuOpen = ref(false);
const isNavigating = ref(false); // State untuk efek Blur saat pindah section

const toggleTheme = () => {
  isDark.value = !isDark.value;
  document.documentElement.classList.toggle('dark', isDark.value);
};
const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

// Fungsi navigasi mulus (Warp Speed Blur Effect)
const navigateTo = (e, targetId) => {
  e.preventDefault();
  
  // Memicu efek kaca pecah secara manual di koordinat klik tombol
  handleGlobalClick(e);

  // Mengaktifkan efek Blur / Warp
  isNavigating.value = true;
  
  const target = document.querySelector(targetId);
  if (target) {
    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }

  // Tutup menu mobile jika sedang terbuka
  if (isMobileMenuOpen.value) {
    isMobileMenuOpen.value = false;
  }

  // Matikan efek blur setelah scroll selesai (600ms)
  setTimeout(() => {
    isNavigating.value = false;
  }, 600);
};

// --- DATA KONTAK ---
const currentYear = new Date().getFullYear();
const contactNodes = ref([
  { role: 'Hardware & OS Node', name: 'Reza Saputro', phone: '6281111111111', photo: 'https://picsum.photos/seed/reza/400/500', colorClass: 'text-blue-400', borderGlow: 'hover:border-blue-500/50 hover:shadow-blue-500/20', btnColor: 'bg-blue-600 hover:bg-blue-500' },
  { role: 'Software & IoT Node', name: 'Ali Sinaga', phone: '6282222222222', photo: 'https://picsum.photos/seed/ali/400/500', colorClass: 'text-emerald-400', borderGlow: 'hover:border-emerald-500/50 hover:shadow-emerald-500/20', btnColor: 'bg-emerald-600 hover:bg-emerald-500' },
  { role: 'Network & Cyber Node', name: 'M. Ridho', phone: '6283333333333', photo: 'https://picsum.photos/seed/ridho/400/500', colorClass: 'text-purple-400', borderGlow: 'hover:border-purple-500/50 hover:shadow-purple-500/20', btnColor: 'bg-purple-600 hover:bg-purple-500' }
]);
</script>

<template>
  <div class="min-h-screen bg-slate-50 dark:bg-slate-950 text-slate-800 dark:text-slate-300 scroll-smooth transition-colors duration-500 overflow-x-hidden relative cursor-none">
    
    <div class="hidden lg:block fixed pointer-events-none z-[100000]" :style="{ left: mouseX + 'px', top: mouseY + 'px' }">
      <div class="absolute -translate-x-1/2 -translate-y-1/2 w-32 h-32 bg-cyan-400/15 blur-[25px] rounded-full transition-transform duration-75 ease-out"></div>
      <div class="absolute -translate-x-1/2 -translate-y-1/2 rounded-full bg-cyan-400 shadow-[0_0_15px_#22d3ee] transition-all duration-150 ease-out"
           :class="isClicking ? 'w-6 h-6 opacity-80' : 'w-2 h-2 opacity-100'"></div>
    </div>

    <div class="hidden lg:block fixed inset-0 pointer-events-none z-[99998] overflow-hidden">
      <div v-for="shatter in shatters" :key="shatter.id" class="absolute shatter-glass" :style="{ left: shatter.x + 'px', top: shatter.y + 'px' }">
        <svg width="120" height="120" viewBox="0 0 100 100" fill="none" stroke="rgba(34, 211, 238, 1)" stroke-width="2">
          <path d="M50 50 L20 10 M50 50 L80 15 M50 50 L90 60 M50 50 L60 95 M50 50 L10 80" stroke-linecap="round"/>
          <path d="M40 40 L30 20 M60 40 L70 25 M60 60 L80 70 M40 60 L20 65" stroke-dasharray="2 4"/>
          <circle cx="50" cy="50" r="2" fill="#fff" />
          <circle cx="20" cy="10" r="1.5" fill="#22d3ee" />
          <circle cx="80" cy="15" r="1.5" fill="#22d3ee" />
          <circle cx="90" cy="60" r="1.5" fill="#22d3ee" />
        </svg>
      </div>
    </div>

    <nav class="fixed w-full z-50 top-0 glass-panel border-b-0 backdrop-blur-xl">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between h-20 items-center">
          
          <div class="flex items-center gap-4">
            <div class="relative w-10 h-10 flex items-center justify-center animate-spin3D cursor-none">
              <div class="absolute inset-0 bg-gradient-to-tr from-cyan-400 to-blue-600 rounded-lg opacity-80 blur-[4px]"></div>
              <div class="absolute inset-0 border border-white/40 rounded-lg bg-white/10 backdrop-blur-sm flex items-center justify-center shadow-[inset_0_0_10px_rgba(255,255,255,0.2)]">
                <span class="text-white font-black font-serif text-xl drop-shadow-md">S</span>
              </div>
            </div>
            
            <div class="flex-shrink-0 font-serif font-black text-2xl tracking-wide cursor-none">
              <span class="text-slate-900 dark:text-white">SELESE</span><span class="text-cyan-500">TECH</span>
            </div>
          </div>
          
          <div class="hidden md:flex items-center space-x-8 text-sm uppercase tracking-widest font-semibold relative z-10">
            <a href="#intro" @click="navigateTo($event, '#intro')" class="hover:text-cyan-400 hover:scale-110 transition-all cursor-none">Intro</a>
            <a href="#operatives" @click="navigateTo($event, '#operatives')" class="hover:text-cyan-400 hover:scale-110 transition-all cursor-none">Operatives</a>
            <a href="#stack" @click="navigateTo($event, '#stack')" class="hover:text-cyan-400 hover:scale-110 transition-all cursor-none">Stack</a>
            <button @click="toggleTheme" class="p-2 rounded-full glass-panel hover:bg-slate-200 dark:hover:bg-slate-800 transition-all cursor-none">
              <span v-if="!isDark">🌙</span><span v-else>☀️</span>
            </button>
          </div>

          <div class="md:hidden flex items-center">
            <button @click="toggleTheme" class="mr-4 p-2 rounded-full glass-panel text-xs cursor-none">
              <span v-if="!isDark">🌙</span><span v-else>☀️</span>
            </button>
            <button @click="toggleMobileMenu" class="text-slate-800 dark:text-white focus:outline-none cursor-none">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path v-if="!isMobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
              </svg>
            </button>
          </div>
        </div>
      </div>

      <div v-if="isMobileMenuOpen" class="md:hidden glass-panel absolute w-full left-0 top-20 border-t border-slate-200 dark:border-slate-800 py-4 px-6 flex flex-col space-y-4 shadow-2xl animate-fadeInUp cursor-none">
        <a href="#intro" @click="navigateTo($event, '#intro')" class="block font-bold uppercase tracking-widest hover:text-cyan-500 cursor-none">Intro</a>
        <a href="#operatives" @click="navigateTo($event, '#operatives')" class="block font-bold uppercase tracking-widest hover:text-cyan-500 cursor-none">Operatives</a>
        <a href="#stack" @click="navigateTo($event, '#stack')" class="block font-bold uppercase tracking-widest hover:text-cyan-500 cursor-none">Stack</a>
        <a href="#initialize" @click="navigateTo($event, '#initialize')" class="block font-bold uppercase tracking-widest text-cyan-500 cursor-none">Initialize Contact</a>
      </div>
    </nav>

    <main :class="{'blur-md opacity-40 scale-95': isNavigating, 'blur-0 opacity-100 scale-100': !isNavigating}" class="transition-all duration-500 ease-in-out">
      <HeroSection />
      <TeamCards />
      <ServiceCatalog />
    </main>

    <footer id="initialize" class="relative pt-24 pb-12 bg-slate-100 dark:bg-slate-950 border-t border-slate-300 dark:border-slate-900 z-10 cursor-none">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16 animate-fadeInUp">
          <h2 class="text-xs font-bold tracking-widest text-cyan-600 dark:text-cyan-500 uppercase mb-3">Secure Comms Channel</h2>
          <h3 class="text-4xl sm:text-5xl font-serif font-bold text-slate-900 dark:text-white">Initialize Project.</h3>
          <p class="mt-4 text-slate-600 dark:text-slate-400 max-w-2xl mx-auto">Pilih saluran komunikasi langsung dengan Node Spesialis kami untuk konsultasi teknis yang tepat sasaran.</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-20">
          <div v-for="(contact, index) in contactNodes" :key="index" class="card-3d-wrap animate-fadeInUp opacity-0 cursor-none" :class="`delay-${(index+1)*100}`" style="animation-fill-mode: forwards;">
            <div class="card-3d glass-panel p-6 rounded-2xl flex flex-col items-center text-center group transition-all duration-500 shadow-lg" :class="contact.borderGlow">
              <div class="w-20 h-20 rounded-full overflow-hidden mb-4 border-2 border-slate-300 dark:border-slate-700 group-hover:border-cyan-400 transition-colors duration-300 relative">
                <div class="absolute inset-0 bg-cyan-500/20 opacity-0 group-hover:opacity-100 transition-opacity z-10"></div>
                <img :src="contact.photo" class="object-cover w-full h-full grayscale group-hover:grayscale-0 transition-all duration-500 transform group-hover:scale-110" />
              </div>
              <div class="text-[10px] font-bold uppercase tracking-widest mb-1" :class="contact.colorClass">{{ contact.role }}</div>
              <h4 class="text-xl font-serif font-bold text-slate-900 dark:text-white mb-6">{{ contact.name }}</h4>
              <a :href="`https://wa.me/${contact.phone}`" target="_blank" class="w-full flex items-center justify-center gap-3 text-white px-6 py-3.5 rounded-xl font-bold transition-all hover:scale-105 hover:shadow-[0_0_20px_rgba(255,255,255,0.2)] cursor-none mt-auto" :class="contact.btnColor">
                <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
                Chat {{ contact.name.split(' ')[0] }}
              </a>
            </div>
          </div>
        </div>

        <div class="glass-panel p-2 rounded-3xl border border-slate-300 dark:border-slate-800 animate-fadeInUp delay-300 opacity-0 relative overflow-hidden group" style="animation-fill-mode: forwards;">
          <div class="absolute inset-0 bg-cyan-500/5 opacity-0 group-hover:opacity-100 transition-opacity pointer-events-none z-10 flex items-center justify-center">
             <div class="w-full h-1 bg-cyan-400/50 shadow-[0_0_15px_#22d3ee] animate-pulse absolute top-1/2 -translate-y-1/2"></div>
          </div>
          <div class="grid grid-cols-1 lg:grid-cols-3 gap-0 h-[400px] rounded-2xl overflow-hidden bg-slate-200 dark:bg-slate-900">
            <div class="p-8 lg:p-12 flex flex-col justify-center bg-slate-100 dark:bg-slate-900 border-b lg:border-b-0 lg:border-r border-slate-300 dark:border-slate-800 z-20">
              <h4 class="text-xs font-bold text-cyan-500 uppercase tracking-widest mb-2 flex items-center gap-2">
                <span class="w-2 h-2 rounded-full bg-cyan-500 animate-pulse"></span> HQ Location
              </h4>
              <h3 class="text-3xl font-serif font-bold text-slate-900 dark:text-white mb-6">SeleseTech Node Hub.</h3>
              <p class="text-slate-600 dark:text-slate-400 text-sm mb-6 leading-relaxed">Pusat perakitan hardware, coding center, dan manajemen server kami. Terbuka untuk konsultasi langsung.</p>
              <div class="space-y-3 text-sm font-medium text-slate-700 dark:text-slate-300">
                <div class="flex items-center gap-3">
                  <div class="w-8 h-8 rounded-full bg-slate-200 dark:bg-slate-800 flex items-center justify-center text-cyan-500 text-xs">📍</div>
                  <span>Jl. Teknologi Canggih No.99, JKT</span>
                </div>
                <div class="flex items-center gap-3">
                  <div class="w-8 h-8 rounded-full bg-slate-200 dark:bg-slate-800 flex items-center justify-center text-cyan-500 text-xs">🕒</div>
                  <span>Senin - Sabtu (09:00 - 18:00)</span>
                </div>
              </div>
            </div>
            <div class="lg:col-span-2 relative h-full min-h-[250px] z-20">
              <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3966.466795454645!2d106.82496411476906!3d-6.175392395529402!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e69f5d2e764b12d%3A0x3d2ad6e1e0e9bcc8!2sMonumen%20Nasional!5e0!3m2!1sid!2sid!4v1680000000000!5m2!1sid!2sid" width="100%" height="100%" style="border:0; filter: contrast(1.2) grayscale(0.2);" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade" class="cursor-none"></iframe>
            </div>
          </div>
        </div>
        
        <div class="mt-16 text-center border-t border-slate-300 dark:border-slate-800 pt-8">
           <p class="text-slate-500 dark:text-slate-600 text-xs tracking-widest uppercase font-bold">© {{ currentYear }} SeleseTech Deployment Unit. All systems operational.</p>
        </div>
      </div>
    </footer>
  </div>
</template>