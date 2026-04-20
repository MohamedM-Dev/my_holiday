<script>
    import { goto } from "$app/navigation";
    import { resolve } from "$app/paths";
    import Icon from "@iconify/svelte";

    let props = $props();

    const navItems = [
        { title: "العامة", icon: "material-symbols:globe-2-question-rounded", path: "/general" },
        { title: "البحث", icon: "material-symbols:tab-search-rounded", path: "/search" },
        { title: "العطل", icon: "material-symbols:in-home-mode-rounded", path: "/" }
    ];
</script>


<div 
    dir="ltr" 
    class="fixed bottom-0 left-0 right-0 w-full h-16 bg-amber-600 text-white flex items-center justify-around px-4 shadow-lg z-50"
>
    {#each navItems as item (item.path)}
        <button 
            class="nav-btn {props.title === item.title ? 'active-nav-bar' : 'unactive-nav-bar'}"
            onclick={() => {
                if (props.title !== item.title) {
                    goto(resolve(item.path));
                }
            }}
            aria-label={item.title}
        >
            <Icon 
                icon={item.icon} 
                class="text-4xl" 
            />
        </button>
    {/each}
</div>