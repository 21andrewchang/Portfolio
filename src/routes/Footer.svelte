<script lang="ts">
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	export let openModal;

	onMount(() => {
		const emailElement = document.getElementById('email');
		const phoneElement = document.getElementById('phone');
		const resumeElement = document.getElementById('resume');

		if (phoneElement) {
			phoneElement.addEventListener('click', function () {
				copyToClipboard('5109358199');
			});
		}
		if (emailElement) {
			emailElement.addEventListener('click', function () {
				copyToClipboard('21andrewch@gmail.com');
			});
		}
		if (resumeElement) {
			resumeElement.addEventListener('click', function () {
				openModal();
				console.log('resume');
			});
		}
	});

	function copyToClipboard(text: string): void {
		navigator.clipboard
			.writeText(text)
			.then(() => {
				console.log('Email copied to clipboard!');
			})
			.catch((error) => {
				console.error('Could not copy email to clipboard.', error);
			});
	}
</script>

<header>
	<nav>
		<ul>
			<li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
				<a href="https://www.linkedin.com/in/andrew-chang-a88b58148/">LinkedIn</a>
			</li>
			<li aria-current={$page.url.pathname === '/about' ? 'page' : undefined}>
				<a id="resume">Resumé</a>
			</li>
			<li aria-current={$page.url.pathname.startsWith('/currently') ? 'page' : undefined}>
				<a id="email">Email</a>
			</li>
			<li aria-current={$page.url.pathname.startsWith('/currently') ? 'page' : undefined}>
				<a id="phone">PhoneNumber</a>
			</li>
		</ul>
	</nav>
</header>

<style>
	header {
		display: flex;
		justify-content: flex-end;
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
		padding-right: 0px;
		height: 100%;
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 0.5rem;
		color: rgba(256, 256, 256, 0.3);
		font-weight: 400;
		font-size: 10px;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: rgba(256, 256, 256, 0.9);
	}

	li:not(:last-child) a::after {
		content: '|';
		margin-left: 0.7rem;
		color: rgba(256, 256, 256, 0.3);
	}

	/* Added styles for dividers before the first child */
	li:first-child a::before {
		content: '|';
		margin-right: 0.7rem;
		color: rgba(256, 256, 256, 0.3);
	}

	/* Added styles for dividers after the last child */
	li:last-child a::after {
		content: '|';
		margin-left: 0.7rem;
		color: rgba(256, 256, 256, 0.3);
	}
</style>
