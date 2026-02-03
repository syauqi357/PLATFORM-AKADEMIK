<script>
  import { onMount } from 'svelte';
  import { animate, stagger } from 'animejs';

  onMount(() => {
    // Animate title
    animate('.hero-title', {
      opacity: [0, 1],
      translateY: [30, 0],
      easing: 'easeOutExpo',
      duration: 1000
    });

    // Animate subtitle
    animate('.hero-subtitle', {
      opacity: [0, 1],
      translateY: [20, 0],
      delay: 300,
      easing: 'easeOutExpo',
      duration: 1000
    });

    // Animate buttons
    animate('.cta-btn', {
      opacity: [0, 1],
      translateY: [20, 0],
      delay: stagger(100, { start: 500 }),
      easing: 'easeOutExpo',
      duration: 800
    });

    // Subtle float for background orbs
    animate('.float-orb', {
      translateY: [-10, 10],
      duration: 4000,
      easing: 'easeInOutSine',
      direction: 'alternate',
      loop: true,
      delay: stagger(500)
    });

    // Animate grid blocks
    animate('.grid-block', {
      opacity: [0, 1],
      scale: [0.5, 1],
      delay: stagger(50, { start: 800 }),
      easing: 'easeOutExpo',
      duration: 600
    });

    // Animate accent lines
    animate('.accent-line', {
      scaleX: [0, 1],
      delay: stagger(100, { start: 600 }),
      easing: 'easeOutExpo',
      duration: 1000
    });
  });
</script>

<div class="relative flex min-h-screen items-center justify-center overflow-hidden bg-slate-950">

  <!-- Grid Pattern -->
  <div class="absolute inset-0 bg-[linear-gradient(rgba(255,255,255,0.03)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.03)_1px,transparent_1px)] bg-[size:60px_60px]"></div>

  <!-- Corner Grid Accents -->
  <div class="absolute left-0 top-0 h-64 w-64 border-b border-r border-white/5"></div>
  <div class="absolute right-0 top-0 h-64 w-64 border-b border-l border-white/5"></div>
  <div class="absolute bottom-0 left-0 h-64 w-64 border-t border-r border-white/5"></div>
  <div class="absolute bottom-0 right-0 h-64 w-64 border-t border-l border-white/5"></div>

  <!-- Horizontal Accent Lines -->
  <div class="accent-line absolute left-0 top-1/4 h-px w-32 origin-left bg-linear-to-r from-white/20 to-transparent"></div>
  <div class="accent-line absolute right-0 top-1/3 h-px w-48 origin-right bg-gradient-to-l from-white/20 to-transparent"></div>
  <div class="accent-line absolute left-0 bottom-1/4 h-px w-40 origin-left bg-linear-to-r from-white/20 to-transparent"></div>
  <div class="accent-line absolute right-0 bottom-1/3 h-px w-36 origin-right bg-gradient-to-l from-white/20 to-transparent"></div>

  <!-- Small Grid Blocks -->
  <div class="absolute left-12 top-20 grid grid-cols-3 gap-1">
    <div class="grid-block h-2 w-2 bg-white/30 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/10 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/20 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/10 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/40 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/10 opacity-0"></div>
  </div>
  <div class="absolute right-16 bottom-24 grid grid-cols-3 gap-1">
    <div class="grid-block h-2 w-2 bg-white/20 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/10 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/30 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/40 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/10 opacity-0"></div>
    <div class="grid-block h-2 w-2 bg-white/20 opacity-0"></div>
  </div>

  <!-- Cross markers -->
  <div class="absolute left-1/4 top-16 text-white/10 text-xs font-mono">+</div>
  <div class="absolute right-1/4 top-24 text-white/10 text-xs font-mono">+</div>
  <div class="absolute left-1/3 bottom-20 text-white/10 text-xs font-mono">+</div>
  <div class="absolute right-1/3 bottom-32 text-white/10 text-xs font-mono">+</div>

  <!-- Background Gradient Orbs -->
  <div class="float-orb absolute -top-32 -right-32 h-96 w-96 rounded-full bg-purple-600/20 blur-3xl"></div>
  <div class="float-orb absolute -bottom-32 -left-32 h-96 w-96 rounded-full bg-blue-600/20 blur-3xl"></div>

  <!-- Content -->
  <div class="relative z-10 px-6 text-center">
    <h1 class="hero-title  mb-6 text-5xl font-bold tracking-tight text-white opacity-0 md:text-6xl lg:text-7xl">
      Platform Akademik
    </h1>

    <p class="hero-subtitle mx-auto mb-10 max-w-xl text-lg text-slate-400 opacity-0">
      Platform informasi akademik terpadu untuk mendukung kegiatan belajar mengajar
    </p>

    <div class="flex flex-col items-center justify-center gap-4 sm:flex-row">
      <button class="cta-btn rounded-lg bg-white px-8 py-3 font-medium text-slate-900 opacity-0 transition hover:bg-slate-100">
        Mulai Sekarang
      </button>
      <button class="cta-btn rounded-lg border border-slate-700 px-8 py-3 font-medium text-white opacity-0 transition hover:border-slate-500 hover:bg-slate-800/50">
        Pelajari Lebih Lanjut
      </button>
    </div>
  </div>
</div>
