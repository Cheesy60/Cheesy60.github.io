<script>
	import { page } from '$app/state';
	let { children } = $props();
	import "../app.css"
	
	let links = {"Home" : '/', "Art Gallery" : '/arts', "3D Renderer" : '/render'}
</script>



<nav class="bg-[#e3b4f0] w-full justify-center flex gap-12.5 rounded-[30px]">
{#each Object.entries(links) as [key,value]}
<a href= {value} class="rounded-[9px] p-4 no-underline transition-colors {page.url.pathname === value ? 'bg-[#b897d1]' : 'bg-[#f4caffa9]'}">{key}</a>

{/each}
</nav>
{@render children()}