<script lang="ts">
	import { onMount } from 'svelte';

	let selectedProject = 1;
	const projects = [
		{ id: 1, name: 'journal 2', description: 'Description for FPGA Tetris...' },
		{
			id: 2,
			name: 'journal 1',
			description: 'Description for Project 2...'
		},
		{ id: 3, name: 'thoughts on stuff', description: 'Description for Project 3...' },
		{ id: 4, name: 'thoughts on other stuff', description: 'Description for Project 3...' }
	];
	let disabled = false;

	onMount(() => {
		function handleKeyPress(event) {
			const key = event.key.toLowerCase();

			if (key === 'j' && selectedProject < projects.length && !disabled) {
				selectedProject++;
			} else if (key === 'k' && selectedProject > 1 && !disabled) {
				selectedProject--;
			}
		}

		window.addEventListener('keydown', handleKeyPress);

		// Cleanup the event listener when the component is unmounted
		return () => {
			window.removeEventListener('keydown', handleKeyPress);
		};
	});
</script>

<svelte:head>
	<title>currently</title>
</svelte:head>

<h1 class="visually-hidden">currently</h1>

<p>a list of unorganized thoughts</p>
<section class="project-list">
	<div class="scroll-container">
		{#each projects as project}
			<div
				class:selected={selectedProject === project.id}
				on:click={() => (selectedProject = project.id)}
				on:mouseenter={() => {
					disabled = true;
					selectedProject = project.id;
				}}
				on:mouseleave={() => (disabled = false)}
				style="display: flex; cursor: pointer;"
			>
				<p style="margin-right: 20px; line-height: 0;">{project.id}</p>
				<p style="line-height: 0;">{project.name}</p>
			</div>
		{/each}
	</div>
</section>

<style>
	section {
		height: 300px;
	}

	.project-list {
		max-height: 260px; /* Constrain the height */
		overflow-y: auto; /* Enable vertical scrolling */
	}

	.scroll-container {
		overflow-y: auto; /* Enable vertical scrolling */
	}

	.selected {
		background: rgba(256, 256, 256, 0.1);
	}
</style>
