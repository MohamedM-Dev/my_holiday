<script>
	import { resolve } from "$app/paths";

    let { list = $bindable() } = $props();
</script>

{#each list as post (post.id)}
    <a href={resolve(`/${post.id}`)}>
        <div class="bg-white p-4 mb-2 border-b rounded-4xl my-7 min-h-30 mx-3 shadow-lg" dir="rtl">
            <h2 class="text-black font-bold">{post.title}</h2>
            {#if post.thumbnail}
                <img src={post.thumbnail} alt={post.title} class="w-full my-4 rounded-3xl shadow-lg">  
            {/if}
            <p>{post.date}</p>
        </div>
    </a>
{/each}
