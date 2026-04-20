<script>
    // Standard import for Iconify in Svelte
    import Header from '$lib/layout/Header.svelte';
    import Footer from '$lib/layout/Footer.svelte';
	import { API } from '$lib';
	import News from '$lib/layout/News.svelte';
	import Loading from '$lib/layout/LoadingNews.svelte';

    const title = "البحث";
    let query = $state("");
    $inspect(query);
    let list = $state([])
    let loading = $state(true)

    async function onsubmit() {
        try {
            const res = await fetch(`${API}/news/search?q=${query}`)
            list = await res.json()
            loading = false
        } catch (error) {
            console.error("فشل في جلب البيانات:", error)
        }
    }

</script>


<Header {title}/>
<main class="my-20">
    
    <form class="row" {onsubmit}>
        <input bind:value={query} class="w-70 p-4 rounded-4xl shadow-2xl mt-5" type="search" name="search" id="search" placeholder="بحث" dir="rtl">
    </form>

    {#if list.length > 0}
        {#if loading}
            <Loading/>
        {:else}
            <News bind:list />
        {/if}
    {/if}
        


</main>
<Footer {title}/>

