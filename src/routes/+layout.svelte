<script>
	import Header from './Header.svelte';
	import './styles.css';
	import Footer from './Footer.svelte';

	import { page } from '$app/stores';

	window.addEventListener('keydown', (event) => {
		// Check the pressed key
		switch (event.key) {
			case '1':
				page.set({ path: '/' }); // Navigate to the home page
				break;
			case '2':
				page.set({ path: '/projects' }); // Navigate to the projects page
				break;
			case '3':
				page.set({ path: '/currently' }); // Navigate to the currently page
				break;
			default:
				break;
		}
	});
</script>

<div class="app">
	<Header />
	<main>
		<slot />
	</main>

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
</style>
