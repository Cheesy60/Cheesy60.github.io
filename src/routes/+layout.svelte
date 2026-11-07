<script>
	import favicon from '#lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<nav class="navi">
<a href="/">
Home
</a>
<a href="/arts">
Art Gallery
</a>
<a href="/render">
3d renderer
</a>
</nav>
{@render children()}
<style>
:global(body) {
	background-color: lavender;
	font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
	display: flex;
	flex-direction: column;
	align-items: center;

}
.navi {
background-color: aliceblue;
width: 100%;
justify-content: center;
display: flex;
gap: 50px;
border-radius: 30px;
}
.navi a{

border-radius: 9px;
padding: 1rem;
text-decoration: none;
gap: 0px;
background-color:#e0f7ff;

}
.navi a:active{
color: black;
}
.navi a:visited{
color: black;
}


</style>
