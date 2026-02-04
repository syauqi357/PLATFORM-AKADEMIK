<script>
  import Navbar from './lib/navbar.svelte';
  import Homepage from './lib/homepage.svelte';
  import Docs from './lib/docs/documentations.svelte';
  import { currentPage } from './lib/stores/navigation.js';
</script>

<Navbar />

{#if $currentPage === 'home'}
  <Homepage />
{:else if $currentPage === 'docs'}
  <Docs />
{/if}
