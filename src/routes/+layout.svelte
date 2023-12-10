<script>
	import Header from './Header.svelte';
	import './styles.css';
	import Footer from './Footer.svelte';
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
	.app {
		position: relative;
		display: flex;
		flex-direction: column;
		padding-top: 25vh;
		padding-left: 30vh;
		padding-right: 30vh;
		overflow: hidden;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	section {
		height: 300px;
	}
</style>
