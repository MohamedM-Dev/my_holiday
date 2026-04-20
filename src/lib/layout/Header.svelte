<script>
    // من الأفضل تفكيك الخصائص (Destructuring) لسهولة الاستخدام
    let { title } = $props(); 
    
    import Icon from "@iconify/svelte";
    import { page } from '$app/stores'; // استدعاء مخزن الصفحة من SvelteKit
</script>

<div 
    dir="rtl" 
    class="flex items-center justify-between w-full h-16 px-8 bg-amber-600 text-white text-2xl font-bold fixed top-0"
>
    <div class="flex-1 text-center">
        {title}
    </div>
    
    {#if $page.url.pathname !== '/'}
        <button 
            class="active:bg-white/25 transition h-12 w-12 flex items-center justify-center rounded-full"
            onclick={() => history.back()}
        >
            <Icon 
                icon="material-symbols:line-start-arrow" 
                class="text-4xl" 
            />
        </button>
    {/if}
</div>