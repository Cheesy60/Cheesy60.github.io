<script>
	import { page } from '$app/state';
	import "../app.css"
	let { children } = $props();
	
	let links = {"Home" : '/', "Art Gallery" : '/arts', "3D Renderer" : '/render', "3D modelling" : '/3d'}
</script>

<div class="min-h-screen flex flex-col">
<nav class="shrink-0 bg-[#e3b4f0] w-full flex flex-wrap items-center justify-center gap-2 sm:gap-6 px-4 py-2">
  {#each Object.entries(links) as [key, value]}
    <a 
      href={value} 
      class="inline-flex items-center justify-center whitespace-nowrap px-3 py-2 sm:px-4 sm:py-3 text-sm sm:text-base no-underline transition-colors {page.url.pathname === value ? 'bg-[#d197ce59]' : 'bg-[#f4caffa9]'}"
    >
      {key}
    </a>
  {/each}
</nav>

{@render children()}
<style>
:global(html){
	overflow-y: scroll;
}
</div>
</style>
