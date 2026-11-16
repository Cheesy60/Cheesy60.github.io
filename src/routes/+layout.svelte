<script>
	import { page } from '$app/state';
	import "../app.css"
	let { children } = $props();
	
	let links = {"Home" : '/', "Art Gallery" : '/arts', "3D Renderer" : '/render', "3D modelling" : '/3d'}
</script>



<nav class="bg-[#e3b4f0] w-full justify-center flex gap-6">
{#each Object.entries(links) as [key,value]}
<a href= {value} class=" p-3 no-underline transition-colors {page.url.pathname === value ? 'bg-[#d197ce59]' : 'bg-[#f4caffa9]'}">{key}</a>

{/each}
</nav>
<style>
:global(html){
	overflow-y: scroll;
}

</style>
{@render children()}
