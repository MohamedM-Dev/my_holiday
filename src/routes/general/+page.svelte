<script>
    import Header from '$lib/layout/Header.svelte';
    import Footer from '$lib/layout/Footer.svelte';
    import { API } from '$lib';
    import { onMount } from 'svelte';
	import News from '$lib/layout/News.svelte';
	import Loading from '$lib/layout/LoadingNews.svelte';

    const title = "العامة"
    let list = $state([])
    let loading = $state(true)
    
    onMount(async () => {
        try {
            const res = await fetch(`${API}/news`)
            list = await res.json() 
        } catch (error) {
            console.error("فشل في جلب البيانات:", error)
        }
    })
</script>

<Header {title}/>
<main class="my-24">

    {#if list.length > 0}
        {#if loading}
            <Loading/>
        {:else}
            <News bind:list />
        {/if}
    {/if}

</main>
<Footer {title}/>