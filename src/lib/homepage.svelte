<script>
  import { onMount } from 'svelte';
  import { animate, stagger } from 'animejs';

  const words = ['Akademik', 'Madrasah', 'Sekolah', 'Guru', 'Kepala Sekolah'];
  let currentWordIndex = 0;
  let isVisible = true;

  function animateTextChange() {
    isVisible = false;
    setTimeout(() => {
      currentWordIndex = (currentWordIndex + 1) % words.length;
      isVisible = true;
    }, 400);
  }

  onMount(() => {
    // Start text rotation after hero animation completes
    const startTimeout = setTimeout(() => {
      textInterval = setInterval(animateTextChange, 3000);
    }, 2000);
    let textInterval;

    // ============================================
    // LOGO ANIMATION - Simple slide up entrance
    // ============================================

    // Animate logo container - slide up from bottom with fade
    animate('.logo-container', {
      opacity: [0, 1],
      translateY: [40, 0],
      duration: 1000,
      easing: 'easeOutExpo',
    });

    // Stagger the polygon pieces slightly for a nice reveal
    animate('.logo-polygon', {
      opacity: [0, 1],
      translateY: [20, 0],
      delay: stagger(100, { start: 200 }),
      duration: 800,
      easing: 'easeOutExpo',
    });

    // Glow fade in
    animate('.logo-glow', {
      opacity: [0, 0.4],
      duration: 1200,
      delay: 500,
      easing: 'easeOutQuad',
    });

    // ============================================
    // OUTLINE SVG ANIMATION - Looping line draw
    // ============================================

    // Fade in the outline container
    animate('.outline-container', {
      opacity: [0, 1],
      duration: 1000,
      delay: 300,
      easing: 'easeOutQuad',
    });

    // Set initial stroke state and create looping draw animation
    const outlineLines = document.querySelectorAll('.outline-line');
    outlineLines.forEach((line, index) => {
      const length = line.getTotalLength();
      line.style.strokeDasharray = length;
      line.style.strokeDashoffset = length;

      // Looping line draw: draw in -> pause -> draw out -> pause -> repeat
      animate(line, {
        strokeDashoffset: [length, 0, 0, -length, -length, length],
        delay: index * 150,
        duration: 5000,
        easing: 'easeInOutSine',
        loop: true,
      });
    });

    // Animate title
    animate('.hero-title', {
      opacity: [0, 1],
      translateY: [30, 0],
      easing: 'easeOutExpo',
      duration: 1000,
      delay: 800,
    });

    // Animate subtitle
    animate('.hero-subtitle', {
      opacity: [0, 1],
      translateY: [20, 0],
      delay: 1000,
      easing: 'easeOutExpo',
      duration: 1000,
    });

    // Animate buttons
    animate('.cta-btn', {
      opacity: [0, 1],
      translateY: [20, 0],
      delay: stagger(100, { start: 1200 }),
      easing: 'easeOutExpo',
      duration: 800,
    });

    // Animate grid blocks
    animate('.grid-block', {
      opacity: [0, 1],
      scale: [0.5, 1],
      delay: stagger(50, { start: 800 }),
      easing: 'easeOutExpo',
      duration: 600,
    });

    // Animate accent lines
    animate('.accent-line', {
      scaleX: [0, 1],
      delay: stagger(100, { start: 600 }),
      easing: 'easeOutExpo',
      duration: 1000,
    });

    return () => {
      clearTimeout(startTimeout);
      if (textInterval) clearInterval(textInterval);
    };
  });
</script>

<div
  class="relative flex min-h-screen items-center justify-center overflow-hidden bg-slate-900"
>
  <!-- Grid Pattern -->
  <div
    class="absolute inset-0 bg-[linear-gradient(rgba(255,255,255,0.03)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.03)_1px,transparent_1px)] bg-size-[60px_60px]"
  ></div>

  <!-- Corner Grid Accents -->
  <div
    class="absolute left-0 top-0 h-64 w-64 border-b border-r border-white/5"
  ></div>
  <div
    class="absolute right-0 top-0 h-64 w-64 border-b border-l border-white/5"
  ></div>
  <div
    class="absolute bottom-0 left-0 h-64 w-64 border-t border-r border-white/5"
  ></div>
  <div
    class="absolute bottom-0 right-0 h-64 w-64 border-t border-l border-white/5"
  ></div>

  <!-- Horizontal Accent Lines -->
  <div
    class="accent-line absolute left-0 top-1/4 h-px w-32 origin-left bg-linear-to-r from-white/20 to-transparent"
  ></div>
  <div
    class="accent-line absolute right-0 top-1/3 h-px w-48 origin-right bg-linear-to-l from-white/20 to-transparent"
  ></div>
  <div
    class="accent-line absolute left-0 bottom-1/4 h-px w-40 origin-left bg-linear-to-r from-white/20 to-transparent"
  ></div>
  <div
    class="accent-line absolute right-0 bottom-1/3 h-px w-36 origin-right bg-linear-to-l from-white/20 to-transparent"
  ></div>

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
  <div class="absolute left-1/3 bottom-20 text-white/10 text-xs font-mono">
    +
  </div>
  <div class="absolute right-1/3 bottom-32 text-white/10 text-xs font-mono">
    +
  </div>

  <!-- Background Gradient Orbs -->
  <!--  <div class="float-orb absolute -top-32 -right-32 h-96 w-96 rounded-full bg-purple-600/20 blur-3xl"></div>-->
  <!--  <div class="float-orb absolute -bottom-32 -left-32 h-96 w-96 rounded-full bg-blue-600/20 blur-3xl"></div>-->

  <!-- Grid Lines Background - Static sliced effect -->
  <div
    class="outline-container absolute inset-0 flex items-center justify-center pointer-events-none opacity-0"
  >
    <svg
      class="w-full h-full max-w-4xl max-h-[80vh]"
      viewBox="0 0 239.12 161.18"
      xmlns="http://www.w3.org/2000/svg"
      preserveAspectRatio="xMidYMid slice"
    >
      <!-- Vertical lines -->
      <line
        class="outline-line"
        x1="85.35"
        y1="78.71"
        x2="85.35"
        y2="143.27"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="153.52"
        y1="78.7"
        x2="153.52"
        y2="147.15"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <!-- Diagonal lines / \ -->
      <line
        class="outline-line"
        x1="74.42"
        y1="123.39"
        x2="139.81"
        y2="161.11"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="164.55"
        y1="123.21"
        x2="99.17"
        y2="160.92"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="0.04"
        y1="41.08"
        x2="172.4"
        y2="140.5"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="238.85"
        y1="40.76"
        x2="66.5"
        y2="140.17"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="0.18"
        y1="99.49"
        x2="172.54"
        y2="0.08"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="238.99"
        y1="99.49"
        x2="66.64"
        y2="0.08"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="0.27"
        y1="139.35"
        x2="172.62"
        y2="39.94"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
      <line
        class="outline-line"
        x1="239.08"
        y1="139.35"
        x2="66.72"
        y2="39.94"
        fill="none"
        stroke="currentColor"
        stroke-miterlimit="10"
        stroke-width="0.3"
      />
    </svg>
  </div>

  <!-- Content -->
  <div class="relative z-10 px-6 text-center">
    <!-- Animated Logo Section -->
    <div class="logo-container mb-8 flex justify-center opacity-0">
      <div class="logo-wrapper relative">
        <!-- Glow effect behind logo -->
        <div
          class="logo-glow absolute inset-0 -m-8 rounded-full bg-purple-500/30 blur-2xl opacity-0"
        ></div>

        <!-- Main Logo SVG -->
        <svg
          class="w-24 h-20 md:w-32 md:h-28 lg:w-40 lg:h-36 relative z-10"
          viewBox="0 0 137.27 118.67"
          xmlns="http://www.w3.org/2000/svg"
        >
          <polygon
            class="logo-polygon"
            points="137.27 39.46 102.78 59.36 102.76 59.37 68.93 39.86 34.61 59.65 34.59 59.66 0 39.71 34.34 19.9 68.85 0 103.44 19.95 137.27 39.46"
            fill="#1C4D8D"
          />
          <polygon
            class="logo-polygon"
            points="102.78 59.38 102.78 98.95 102.75 98.97 68.43 79.17 102.76 59.37 102.78 59.38"
            fill="#BDE8F5"
          />
          <polygon
            class="logo-polygon"
            points="102.75 98.97 68.59 118.67 34.61 99.07 34.61 59.66 68.43 79.17 102.75 98.97"
            fill="#4988C4"
          />
        </svg>
      </div>
    </div>
    <h1
      class="hero-title mb-6 text-5xl font-bold tracking-tight text-white opacity-0 md:text-6xl lg:text-7xl"
    >
      Platform <span
        class="inline-block text-emerald-300 transition-all duration-300 ease-in-out"
        class:opacity-0={!isVisible}
        class:translate-y-2={!isVisible}>{words[currentWordIndex]}</span
      >
    </h1>

    <p
      class="hero-subtitle mx-auto mb-10 max-w-xl text-lg text-slate-400 opacity-0"
    >
      Platform informasi akademik terpadu untuk mendukung kegiatan belajar
      mengajar
    </p>

    <div class="flex flex-col items-center justify-center gap-4 sm:flex-row">
      <button
        class="capitalize cta-btn rounded-lg bg-white px-8 py-3 font-medium text-slate-900 opacity-0 transition hover:bg-slate-100"
      >
        download
      </button>
      <button
        class="cta-btn backdrop-blur-xs rounded-lg border border-slate-700 px-8 py-3 font-medium text-white opacity-0 transition hover:border-slate-500 hover:bg-slate-800/50"
      >
        contribute
      </button>
    </div>
  </div>
</div>

<style>
  .logo-polygon {
    transform-origin: center;
    transform-box: fill-box;
  }

  .outline-line {
    stroke: rgba(255, 255, 255, 0.15);
  }

  .outline-container {
    color: rgba(255, 255, 255, 0.15);
  }
</style>
