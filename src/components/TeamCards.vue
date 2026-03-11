<script setup>
import { ref } from 'vue';

const team = ref([
  {
    role: 'Hardware & OS Deployment', name: 'Reza Saputro',
    shortBio: 'Pawang hardware. Spesialis HPC & pemulihan data kritis.',
    photo: 'https://picsum.photos/seed/reza/400/500',
    fullBio: 'Reza memiliki pengalaman panjang mendiagnosis kerusakan tingkat komponen. Dari merakit rig liquid cooling yang kompleks hingga menyelamatkan database perusahaan yang terkena enkripsi Ransomware, Reza adalah benteng pertahanan fisik pertama SeleseTech.',
    // SOSMED: Menggunakan link dummy
    socials: { linkedin: '#', github: '#', instagram: '#' },
    skills: ['PC Building', 'Data Recovery', 'OS Hardening', 'Micro-soldering'],
    projects: [
      { title: 'Render Farm Studio Animasi', desc: 'Merakit 20 node workstation berspesifikasi Ryzen Threadripper.' },
      { title: 'Corporate Malware Purge', desc: 'Pemulihan data sensitif dari serangan trojan tanpa membayar ransom.' }
    ]
  },
  {
    role: 'Software Architecture & IoT', name: 'Ali Sinaga',
    shortBio: 'Arsitek kode lintas platform & sistem otomasi fisik.',
    photo: 'https://picsum.photos/seed/ali/400/500',
    fullBio: 'Pengembang Fullstack yang juga menguasai papan sirkuit. Ali membangun fondasi digital menggunakan Laravel (Backend) dan Flutter (Mobile). Proyek andalannya adalah integrasi aplikasi dengan perangkat fisik Internet of Things (IoT) berbasis ESP32 untuk otomasi industri.',
    socials: { linkedin: '#', github: '#', instagram: '#' },
    skills: ['Flutter/Dart', 'Laravel/PHP', 'ESP32/C++', 'System Design'],
    projects: [
      { title: 'Smart Agriculture Node', desc: 'Pemantauan lahan pertanian berbasis tenaga surya & sensor kelembaban ESP32.' },
      { title: 'Enterprise ERP App', desc: 'Aplikasi manajemen perusahaan lintas platform (Android, iOS, Web).' }
    ]
  },
  {
    role: 'Network Security Architect', name: 'M. Ridho',
    shortBio: 'Penjaga gerbang lalu lintas data & topologi jaringan.',
    photo: 'https://picsum.photos/seed/ridho/400/500',
    fullBio: 'Dengan latar belakang Cyber Security, Ridho merancang topologi jaringan yang tahan banting (zero-downtime). Ahli menggunakan infrastruktur MikroTik dan Cisco, ia memastikan lalu lintas data aman, terenkripsi, dan bebas dari bottleneck yang menghambat produktivitas.',
    socials: { linkedin: '#', github: '#', instagram: '#' },
    skills: ['MikroTik RouterOS', 'Cisco Switching', 'Penetration Testing', 'Fiber Optic'],
    projects: [
      { title: '10-Story FO Backbone', desc: 'Penarikan jaringan Fiber Optic tulang punggung untuk gedung perkantoran.' },
      { title: 'Banking Security Audit', desc: 'Pentesting dan hardening server untuk mencegah eksploitasi SQL Injection.' }
    ]
  }
]);

const activeMember = ref(null);

const openModal = (member) => { 
  activeMember.value = member; 
  document.body.style.overflow = 'hidden'; 
};

const closeModal = () => { 
  activeMember.value = null; 
  document.body.style.overflow = 'auto'; 
};
</script>

<template>
  <section id="operatives" class="py-24 relative z-20">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
      <div class="text-center mb-20 animate-fadeInUp">
        <h2 class="text-4xl sm:text-5xl font-serif font-bold text-slate-900 dark:text-white transition-colors duration-300">Core Operatives.</h2>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-10">
        <div v-for="(person, index) in team" :key="index" @click="openModal(person)"
             class="card-3d-wrap animate-fadeInUp opacity-0" :class="`delay-${(index+1)*100}`" style="animation-fill-mode: forwards;">
          <div class="card-3d glass-panel p-8 rounded-2xl h-full flex flex-col group border border-slate-200 dark:border-slate-800 transition-all hover:border-cyan-500/30 overflow-hidden relative">
            
            <div class="absolute inset-0 bg-gradient-to-br from-cyan-600/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>

            <div class="w-24 h-24 rounded-full overflow-hidden mb-8 border-2 border-cyan-500/50 group-hover:border-cyan-400 group-hover:glow-pulse transition-all duration-300 relative z-10">
              <img :src="person.photo" alt="Photo" class="object-cover w-full h-full grayscale group-hover:grayscale-0 group-hover:scale-110 transition-all duration-700 pointer-events-none" />
            </div>
            
            <div class="relative z-10 flex flex-col h-full">
                <div class="inline-block px-3 py-1 rounded-full bg-cyan-100 dark:bg-slate-800 text-xs font-bold text-cyan-800 dark:text-cyan-400 mb-4 border border-cyan-200 dark:border-slate-700 transition-colors self-start">
                    {{ person.role }}
                </div>
                <h3 class="text-2xl font-serif font-bold text-slate-900 dark:text-white mb-3 tracking-tight group-hover:text-cyan-500 dark:group-hover:text-cyan-400 transition-colors">{{ person.name }}</h3>
                <p class="text-slate-600 dark:text-slate-400 text-sm mb-6 leading-relaxed">{{ person.shortBio }}</p>
                <div class="mt-auto text-cyan-700 dark:text-cyan-400 text-sm font-semibold flex items-center gap-2 group-hover:gap-3 transition-all relative z-10">
                    Deploy Full Profile <span class="text-xl">→</span>
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <Teleport to="body">
      <Transition name="backdrop">
          <div v-if="activeMember" class="fixed inset-0 z-[99998] bg-slate-950/90 backdrop-blur-md cursor-none" @click="closeModal"></div>
      </Transition>

      <Transition name="flip">
          <div v-if="activeMember" class="fixed inset-0 z-[99999] flex items-center justify-center p-4 sm:p-6 lg:p-10 cursor-none overscroll-contain" @click="closeModal">
              
              <div class="relative w-full max-w-6xl max-h-[90dvh] bg-slate-100 dark:bg-slate-950 rounded-2xl shadow-2xl overflow-y-auto border border-slate-200 dark:border-cyan-900/50 custom-scrollbar flex flex-col md:flex-row shadow-cyan-500/5 cursor-none" @click.stop>
                  
                  <button @click="closeModal" class="absolute top-5 right-5 z-50 w-12 h-12 rounded-full glass-panel bg-slate-900/80 border border-slate-700 text-white flex items-center justify-center hover:bg-cyan-500 hover:scale-110 transition-all text-2xl font-black">✕</button>
                  
                  <div class="md:w-[35%] bg-slate-200 dark:bg-slate-900 md:sticky top-0 h-auto md:h-full border-b md:border-b-0 md:border-r border-slate-300 dark:border-slate-800">
                    <div class="h-80 md:h-[65%] w-full relative">
                      <div class="absolute inset-0 bg-gradient-to-t from-slate-200 dark:from-slate-900 via-transparent to-transparent md:hidden z-10"></div>
                      <img :src="activeMember.photo" class="object-cover w-full h-full opacity-90 dark:opacity-70 grayscale group-hover:grayscale-0 transition-opacity" />
                    </div>
                    
                    <div class="p-8 md:h-[35%] flex flex-col justify-center bg-slate-100 dark:bg-slate-950">
                      <h4 class="text-cyan-600 dark:text-cyan-400 font-bold tracking-widest uppercase text-xs mb-5">Jaringan Operatif</h4>
                      <div class="flex gap-5">
                        
                        <a :href="activeMember.socials.linkedin" target="_blank" class="w-12 h-12 rounded-full border border-slate-300 dark:border-slate-700 flex items-center justify-center hover:bg-cyan-500 hover:border-cyan-500 hover:scale-110 hover:shadow-cyan-500/20 shadow-md transition-all duration-300 text-slate-600 dark:text-white hover:text-white" title="LinkedIn">
                          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 448 512"><path d="M100.28 448H7.4V148.9h92.88zM53.79 108.1C24.09 108.1 0 83.5 0 53.8a53.79 53.79 0 1 1 107.58 0c0 29.7-24.1 54.3-53.79 54.3zM447.9 448h-92.68V302.4c0-34.7-.7-79.2-48.29-79.2-48.29 0-55.69 37.7-55.69 76.7V448h-92.78V148.9h89.08v40.8h1.3c12.4-23.5 42.69-48.3 87.88-48.3 94 0 111.28 61.9 111.28 142.3V448z"/></svg>
                        </a>
                        
                        <a :href="activeMember.socials.github" target="_blank" class="w-12 h-12 rounded-full border border-slate-300 dark:border-slate-700 flex items-center justify-center hover:bg-slate-800 hover:border-slate-800 hover:scale-110 hover:shadow-slate-800/20 shadow-md transition-all duration-300 text-slate-600 dark:text-white hover:text-white" title="GitHub">
                          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 496 512"><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 389.9 8 244.8 8zM106.9 397.7c-1.3 1-1 3.9 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1.6 1.3-1 1-3.9-1.3-6.2-2.3-2.3-5.2-2.6-6.5-1.6zm-10.7-10.9c-.3 2 1.3 4.3 4.3 4.9 2.6.7 5.2-.3 5.9-2.3.3-2-1.3-4.3-4.3-4.9-2.6-.7-5.2.3-5.9 2.3zm19.8-14.6c-1 2 .3 4.6 2.6 5.9 2 1.3 4.9.7 5.9-1.3 1-2-.3-4.6-2.6-5.9-2-1.3-4.9-.7-5.9 1.3z"/></svg>
                        </a>
                        
                        <a :href="activeMember.socials.instagram" target="_blank" class="w-12 h-12 rounded-full border border-slate-300 dark:border-slate-700 flex items-center justify-center hover:bg-gradient-to-br hover:from-purple-600 hover:to-pink-500 hover:border-transparent hover:scale-110 hover:shadow-pink-500/20 shadow-md transition-all duration-300 text-slate-600 dark:text-white hover:text-white" title="Instagram">
                          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 448 512"><path d="M224.1 141c-63.6 0-114.9 51.3-114.9 114.9s51.3 114.9 114.9 114.9S339 319.5 339 255.9 287.7 141 224.1 141zm0 189.6c-41.1 0-74.7-33.5-74.7-74.7s33.5-74.7 74.7-74.7 74.7 33.5 74.7 74.7-33.6 74.7-74.7 74.7zm146.4-194.3c0 14.9-12 26.8-26.8 26.8-14.9 0-26.8-12-26.8-26.8s12-26.8 26.8-26.8 26.8 12 26.8 26.8zm76.1 27.2c-1.7-35.9-9.9-67.7-36.2-93.9-26.2-26.2-58-34.4-93.9-36.2-37-2.1-147.9-2.1-184.9 0-35.8 1.7-67.6 9.9-93.9 36.1s-34.4 58-36.2 93.9c-2.1 37-2.1 147.9 0 184.9 1.7 35.9 9.9 67.7 36.2 93.9s58 34.4 93.9 36.2c37 2.1 147.9 2.1 184.9 0 35.9-1.7 67.7-9.9 93.9-36.2 26.2-26.2 34.4-58 36.2-93.9 2.1-37 2.1-147.8 0-184.8zM398.8 388c-7.8 19.6-22.9 34.7-42.6 42.6-29.5 11.7-99.5 9-132.1 9s-102.7 2.6-132.1-9c-19.6-7.8-34.7-22.9-42.6-42.6-11.7-29.5-9-99.5-9-132.1s-2.6-102.7 9-132.1c7.8-19.6 22.9-34.7 42.6-42.6 29.5-11.7 99.5-9 132.1-9s102.7-2.6 132.1 9c19.6 7.8 34.7 22.9 42.6 42.6 11.7 29.5 9 99.5 9 132.1s2.7 102.7-9 132.1z"/></svg>
                        </a>
                      </div>
                    </div>
                  </div>

                  <div class="p-8 md:p-14 md:w-[65%] text-slate-800 dark:text-slate-300">
                    <div class="text-xs font-bold text-cyan-600 dark:text-cyan-500 uppercase tracking-widest mb-2 mt-2 md:mt-0">{{ activeMember.role }}</div>
                    <h3 class="text-4xl sm:text-5xl font-serif font-bold mb-8 text-slate-950 dark:text-white leading-tight tracking-tight">{{ activeMember.name }}</h3>
                    <p class="text-base leading-relaxed mb-12 text-slate-700 dark:text-slate-400 font-medium">{{ activeMember.fullBio }}</p>
                    
                    <div class="mb-12">
                      <h4 class="font-serif font-bold text-2xl mb-5 text-slate-900 dark:text-white flex items-center gap-3"><span class="w-3 h-3 bg-cyan-500 rounded-full animate-pulse"></span> Core Technical Stack</h4>
                      <div class="flex flex-wrap gap-3">
                        <span v-for="skill in activeMember.skills" :key="skill" class="px-4 py-2 bg-slate-200 dark:bg-slate-800 border border-slate-300 dark:border-slate-700 rounded text-sm text-slate-800 dark:text-cyan-300 font-medium">
                          {{ skill }}
                        </span>
                      </div>
                    </div>

                    <div class="pb-10">
                      <h4 class="font-serif font-bold text-2xl mb-7 text-slate-900 dark:text-white flex items-center gap-3"><span class="w-3 h-3 bg-emerald-500 rounded-full animate-pulse"></span> Log Project Eksekusi</h4>
                      <div class="space-y-6">
                        <div v-for="proj in activeMember.projects" :key="proj.title" class="p-6 bg-slate-100 dark:bg-slate-900/50 border border-slate-200 dark:border-slate-800 rounded-xl border-l-4 border-l-cyan-500 hover:border-slate-300 dark:hover:border-slate-700 transition-colors shadow-sm">
                          <h5 class="text-lg font-bold text-slate-950 dark:text-white mb-2 leading-tight">{{ proj.title }}</h5>
                          <p class="text-sm text-slate-600 dark:text-slate-400 leading-relaxed">{{ proj.desc }}</p>
                        </div>
                      </div>
                    </div>
                  </div>
              </div>
          </div>
      </Transition>
    </Teleport>
  </section>
</template>

<style scoped>
/* Scrollbar khusus untuk modal portofolio */
.custom-scrollbar::-webkit-scrollbar { width: 5px; }
.custom-scrollbar::-webkit-scrollbar-track { background: rgba(10, 15, 28, 0.8); border-radius: 10px; }
.custom-scrollbar::-webkit-scrollbar-thumb { background: #06b6d4; border-radius: 10px; }
.custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #22d3ee; }
</style>