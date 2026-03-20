<script>
	import './layout.css';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href="/assets/favicon/favicon.svg?v=2" /></svelte:head>
{@render children()}
