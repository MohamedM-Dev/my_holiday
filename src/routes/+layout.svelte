<script>
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { App } from '@capacitor/app';
	
	App.addListener('backButton', ({ canGoBack }) => {
		if (canGoBack) {
			// Navigate back if there is history
			window.history.back();
		} else {
			// Exit the app if on the root page
			App.exitApp();
		}
	});


	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>
{@render children()}
