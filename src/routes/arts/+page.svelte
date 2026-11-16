<script>

let images = ["isaac.gif", "GreyCat.png", "aplle.png", "sythe.gif", "trash1.png"]
</script>
<h1 class="text-center p-7 w-full ">My drawings n stuff</h1>

<div class="grid grid-cols-2 gap-5">
    {#each images as src}
    <img {src}  alt = "whatever" class="flex w-auto">
    {/each}
</div>
