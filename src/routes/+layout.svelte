<script>
	import Header from './Header.svelte';
	import './styles.css';
	import Footer from './Footer.svelte';
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
