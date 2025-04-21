<script>
	import Header from '../lib/components/Header.svelte';
	import './styles.css';
	import Footer from '../lib/components/Footer.svelte';
	import { onMount } from 'svelte';

	onMount(() => {
		document.body.style.overflow = 'hidden';
	});
</script>

<div class="app">
	<Header />
	<section>
		<main>
			<slot />
		</main>
	</section>
	<Footer />
</div>

<style>
	html,
	body {
		height: 100%;
		margin: 0;
		padding: 0;
	}

	.app {
		display: flex;
		flex-direction: column;
		width: 100%;
		max-width: 64rem; /* optional, limits width */
		height: 100%; /* or set a specific height */
		box-sizing: border-box;
		justify-content: center;
	}
</style>
