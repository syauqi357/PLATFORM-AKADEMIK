<script>
  let isMenuOpen = false;

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }
</script>

<nav
  class="fixed top-0 left-0 right-0 z-50 bg-transparent backdrop-blur-xs border-b border-white/5"
>
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex items-center justify-between h-16">
      <!-- Logo -->
      <a href="/" class="flex items-center gap-3">
        <svg
          class="w-8 h-7"
          viewBox="0 0 137.27 118.67"
          xmlns="http://www.w3.org/2000/svg"
        >
          <polygon
            points="137.27 39.46 102.78 59.36 102.76 59.37 68.93 39.86 34.61 59.65 34.59 59.66 0 39.71 34.34 19.9 68.85 0 103.44 19.95 137.27 39.46"
            fill="#1C4D8D"
          />
          <polygon
            points="102.78 59.38 102.78 98.95 102.75 98.97 68.43 79.17 102.76 59.37 102.78 59.38"
            fill="#BDE8F5"
          />
          <polygon
            points="102.75 98.97 68.59 118.67 34.61 99.07 34.61 59.66 68.43 79.17 102.75 98.97"
            fill="#4988C4"
          />
        </svg>
        <span class="text-white font-semibold text-lg">Platform Akademik</span>
      </a>

      <!-- Desktop Navigation -->
      <div class="hidden md:flex items-center gap-8">
        <a
          href="#features"
          class="text-slate-400 hover:text-white transition-colors">Features</a
        >
        <a
          href="#about"
          class="text-slate-400 hover:text-white transition-colors">About</a
        >
        <a
          href="#docs"
          class="text-slate-400 hover:text-white transition-colors">Docs</a
        >
        <a
          href="https://github.com"
          aria-label="Github"
          target="_blank"
          rel="noopener noreferrer"
          class="text-slate-400 hover:text-white transition-colors"
        >
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
            <path
              d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
            />
          </svg>
        </a>
      </div>

      <!-- Desktop CTA -->
      <div class="hidden md:block">
        <a
          href="#download"
          class="rounded-lg bg-white px-4 py-2 text-sm font-medium text-slate-900 transition hover:bg-slate-100"
        >
          Download
        </a>
      </div>

      <!-- Mobile Menu Button -->
      <button
        class="md:hidden text-slate-400 hover:text-white transition-colors"
        on:click={toggleMenu}
        aria-label="Toggle menu"
      >
        {#if isMenuOpen}
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>
        {:else}
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16M4 18h16"
            />
          </svg>
        {/if}
      </button>
    </div>
  </div>

  <!-- Mobile Menu -->
  {#if isMenuOpen}
    <div
      class="md:hidden bg-transparent backdrop-blur-xs border-t border-white/5"
    >
      <div class="px-4 py-4 space-y-3">
        <a
          href="#features"
          class="block text-slate-400 hover:text-white transition-colors py-2"
          >Features</a
        >
        <a
          href="#about"
          class="block text-slate-400 hover:text-white transition-colors py-2"
          >About</a
        >
        <a
          href="#docs"
          class="block text-slate-400 hover:text-white transition-colors py-2"
          >Docs</a
        >
        <a
          href="https://github.com"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 text-slate-400 hover:text-white transition-colors py-2"
        >
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
            <path
              d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
            />
          </svg>
          GitHub
        </a>
        <div class="pt-2">
          <a
            href="#download"
            class="block w-full text-center rounded-lg bg-white px-4 py-2 text-sm font-medium text-slate-900 transition hover:bg-slate-100"
          >
            Download
          </a>
        </div>
      </div>
    </div>
  {/if}
</nav>
