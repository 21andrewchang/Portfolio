<script lang="ts">
	import { onMount } from 'svelte';

	import { page } from '$app/stores';
	import { goto } from '$app/navigation';

	let pages = ['/', '/projects', '/currently'];
	let pagePath = 0;
	function navigateTo(path: string) {
		goto(path);
	}

	onMount(() => {
		// This code will run only in the browser, not during SSR
		window.addEventListener('keydown', (event) => {
			switch (event.key) {
				case 'l':
					if (pagePath == 2) {
						pagePath = 0;
					} else {
						pagePath++;
					}
					navigateTo(pages[pagePath]);
					break;
				case 'h':
					if (pagePath == 0) {
						pagePath = 2;
					} else {
						pagePath--;
					}
					navigateTo(pages[pagePath]);
					break;

				default:
					break;
			}
		});
	});
</script>

<header>
	<nav>
		<ul>
			<li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
				<a href="/">andrew ch.</a>
			</li>
			<li aria-current={$page.url.pathname === '/projects' ? 'page' : undefined}>
				<a href="/projects">projects.</a>
			</li>
			<li aria-current={$page.url.pathname.startsWith('/currently') ? 'page' : undefined}>
				<a href="/currently">currently.</a>
			</li>
		</ul>
	</nav>
</header>

<style>
	header {
		display: flex;
	}

	nav {
		display: flex;
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		padding-right: 30px;
		height: 100%;
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		color: rgba(256, 256, 256, 0.3);
		font-weight: 400;
		font-size: 18px;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	li[aria-current='page'] a {
		color: rgba(256, 256, 256, 0.9);
	}

	a:hover {
		color: rgba(256, 256, 256, 0.9);
	}
</style>
