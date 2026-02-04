<script>
  import { onMount } from 'svelte';
  import { marked } from 'marked';
  import { currentPage } from '../stores/navigation.js';

  // Import markdown files as raw text
  import gettingStartedMd from '../../docsmd/getting-started.md?raw';
  import installationMd from '../../docsmd/installation.md?raw';
  import configurationMd from '../../docsmd/configuration.md?raw';
  import usageMd from '../../docsmd/usage.md?raw';
  import apiReferenceMd from '../../docsmd/API-reference.md?raw';

  const sections = [
    {
      id: 'getting-started',
      label: 'Getting Started',
      icon: 'bolt',
      gradient: 'from-blue-500 to-cyan-500',
      content: gettingStartedMd,
    },
    {
      id: 'installation',
      label: 'Installation',
      icon: 'download',
      gradient: 'from-violet-500 to-purple-500',
      content: installationMd,
    },
    {
      id: 'configuration',
      label: 'Configuration',
      icon: 'cog',
      gradient: 'from-amber-500 to-orange-500',
      content: configurationMd,
    },
    {
      id: 'usage',
      label: 'Usage',
      icon: 'play',
      gradient: 'from-emerald-500 to-teal-500',
      content: usageMd,
    },
    {
      id: 'api',
      label: 'API Reference',
      icon: 'code',
      gradient: 'from-pink-500 to-rose-500',
      content: apiReferenceMd,
    },
  ];

  let activeSection = 'getting-started';

  // Configure marked for better code highlighting
  marked.setOptions({
    gfm: true,
    breaks: true,
  });

  function parseMarkdown(content) {
    return marked(content);
  }

  function scrollToSection(id) {
    activeSection = id;
    document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' });
  }

  // Icon components as SVG paths
  const icons = {
    bolt: 'M13 10V3L4 14h7v7l9-11h-7z',
    download: 'M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4',
    cog: 'M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z M15 12a3 3 0 11-6 0 3 3 0 016 0z',
    play: 'M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z M21 12a9 9 0 11-18 0 9 9 0 0118 0z',
    code: 'M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4',
  };
</script>

<div
  class="min-h-screen bg-gradient-to-b from-slate-950 via-slate-900 to-slate-950"
>
  <!-- Header -->
  <div class="pt-24 pb-12 px-4 border-b border-white/5">
    <div class="max-w-6xl mx-auto">
      <div class="flex items-center gap-2 text-sm text-slate-500 mb-4">
        <button
          on:click={() => currentPage.set('home')}
          class="hover:text-white transition-colors">Home</button
        >
        <span>/</span>
        <span class="text-slate-300">Documentation</span>
      </div>
      <h1 class="text-4xl md:text-5xl font-bold text-white mb-4">
        Documentation
      </h1>
      <p class="text-lg text-slate-400 max-w-2xl">
        Everything you need to get started with Platform Akademik. Learn how to
        install, configure, and make the most of our platform.
      </p>
    </div>
  </div>

  <div class="max-w-6xl mx-auto px-4 py-12">
    <div class="flex flex-col lg:flex-row gap-12">
      <!-- Sidebar -->
      <aside class="lg:w-64 shrink-0">
        <nav class="lg:sticky lg:top-24 space-y-1">
          {#each sections as section}
            <button
              on:click={() => scrollToSection(section.id)}
              class="w-full text-left px-4 py-2 rounded-lg text-sm transition-all {activeSection ===
              section.id
                ? 'bg-blue-500/10 text-blue-400 border-l-2 border-blue-500'
                : 'text-slate-400 hover:text-white hover:bg-white/5'}"
            >
              {section.label}
            </button>
          {/each}
        </nav>
      </aside>

      <!-- Main Content -->
      <main class="flex-1 min-w-0">
        {#each sections as section}
          <section id={section.id} class="mb-16 scroll-mt-24">
            <!-- Section Header with Icon -->
            <div class="flex items-center gap-3 mb-6">
              <div
                class="w-10 h-10 rounded-lg bg-linear-to-br {section.gradient} flex items-center justify-center"
              >
                <svg
                  class="w-5 h-5 text-white"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d={icons[section.icon]}
                  />
                </svg>
              </div>
              <h2 class="text-2xl font-bold text-white m-0">{section.label}</h2>
            </div>

            <!-- Markdown Content -->
            <div
              class="docs-content bg-slate-800/30 rounded-xl p-6 border border-white/5"
            >
              {@html parseMarkdown(section.content)}
            </div>
          </section>
        {/each}
      </main>
    </div>
  </div>

  <!-- Footer -->
  <div class="border-t border-white/5 py-8 px-4">
    <div
      class="max-w-6xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4 text-sm text-slate-500"
    >
      <p>Last updated: February 2026</p>
      <div class="flex items-center gap-4">
        <a
          href="https://github.com"
          target="_blank"
          rel="noopener noreferrer"
          class="hover:text-white transition-colors">GitHub</a
        >
        <span class="text-slate-700">|</span>
        <button
          on:click={() => currentPage.set('home')}
          class="hover:text-white transition-colors">Back to Home</button
        >
      </div>
    </div>
  </div>
</div>

<style>
  /* Markdown content styling */
  .docs-content :global(h1) {
    display: none; /* Hide h1 since we have section headers */
  }

  .docs-content :global(h2) {
    font-size: 1.5rem;
    font-weight: 700;
    color: white;
    margin-top: 2rem;
    margin-bottom: 1rem;
    padding-bottom: 0.5rem;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .docs-content :global(h3) {
    font-size: 1.25rem;
    font-weight: 600;
    color: white;
    margin-top: 1.5rem;
    margin-bottom: 0.75rem;
  }

  .docs-content :global(p) {
    color: rgb(148 163 184);
    line-height: 1.75;
    margin-bottom: 1rem;
  }

  .docs-content :global(a) {
    color: rgb(96 165 250);
    text-decoration: underline;
    text-underline-offset: 2px;
  }

  .docs-content :global(a:hover) {
    color: rgb(147 197 253);
  }

  .docs-content :global(strong) {
    color: white;
    font-weight: 600;
  }

  .docs-content :global(code) {
    background: rgb(30 41 59);
    color: rgb(251 191 36);
    padding: 0.125rem 0.375rem;
    border-radius: 0.25rem;
    font-size: 0.875rem;
    font-family: 'JetBrains Mono', monospace;
  }

  .docs-content :global(pre) {
    background: rgb(15 23 42);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 0.75rem;
    padding: 1rem;
    overflow-x: auto;
    margin: 1rem 0;
  }

  .docs-content :global(pre code) {
    background: transparent;
    padding: 0;
    color: rgb(226 232 240);
    font-size: 0.875rem;
    line-height: 1.7;
  }

  .docs-content :global(ul),
  .docs-content :global(ol) {
    color: rgb(148 163 184);
    margin: 1rem 0;
    padding-left: 1.5rem;
  }

  .docs-content :global(li) {
    margin-bottom: 0.5rem;
  }

  .docs-content :global(blockquote) {
    border-left: 4px solid rgb(59 130 246);
    background: rgba(59, 130, 246, 0.1);
    padding: 1rem;
    margin: 1rem 0;
    border-radius: 0 0.5rem 0.5rem 0;
  }

  .docs-content :global(blockquote p) {
    margin: 0;
    color: rgb(191 219 254);
  }

  .docs-content :global(table) {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
    font-size: 0.875rem;
  }

  .docs-content :global(th) {
    background: rgb(30 41 59);
    color: white;
    font-weight: 600;
    text-align: left;
    padding: 0.75rem 1rem;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .docs-content :global(td) {
    padding: 0.75rem 1rem;
    border-bottom: 1px solid rgba(255, 255, 255, 0.05);
    color: rgb(148 163 184);
  }

  .docs-content :global(tr:hover td) {
    background: rgba(255, 255, 255, 0.02);
  }

  .docs-content :global(hr) {
    border: none;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    margin: 2rem 0;
  }
</style>
