<script>
    import Header from '$lib/layout/Header.svelte';
    import Footer from '$lib/layout/Footer.svelte';
    import { onMount } from 'svelte';
    import { API } from '$lib';
	import { page } from '$app/state';

    const id = page.params.id
    let post = $state({})
    let loading = $state(true)
    
    onMount(async () => {
        try {
            const res = await fetch(`${API}/news/${id}`)
            post = await res.json() 
            loading = false
        } catch (error) {
            console.error("فشل في جلب البيانات:", error)
        }
    })
</script>

<Header title={post.title ? post.title.slice(0, 13) + '...': ''}/>

{#if !loading}

<main class="my-24">

<div dir="auto" class="m-3 bg-white rounded-4xl p-4 shadow-lg">
    <h2 class="text-black font-bold mb-6 text-xl">{post.title}</h2>
    <div>{@html post.description}</div>
</div>

</main>

{:else}
<div class="row mt-[85%]">
    <span class="loading loading-dots loading-xl size-30 text-amber-600"></span>
</div>
{/if}

<Footer/>