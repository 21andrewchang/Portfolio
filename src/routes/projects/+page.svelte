<script>
	//bug where if you hover and use j and k to move theres two highlights
	import { onMount } from 'svelte';
	import NoteModal from '../NoteModal.svelte';

	let isModalOpen = false;
	function closeModal() {
		isModalOpen = false;
	}
	let selectedProject = 1;
	const projects = [
		{
			id: 1,
			name: 'FPGA Tetris',
			description:
				'I developed a Tetris game using SystemVerilog on an FPGA board. The game utilized a matrix-based approach to manage Tetrimino positioning and used clock cycles on the FPGA to progress the game. I implemented block movement, rotation, collision detection, and line clearing logic. By integrating the FPGA board with a VGA interface, the game was displayed in real-time on an external monitor. Controlling the movement of the Tetrimino was done through keyboard control, where I mapped key inputs to the movement in C. '
		},
		{
			id: 2,
			name: 'LeNet-5 Convolutional Layer Optimization',
			description: 'Description for Project 2...'
		},
		{ id: 3, name: 'Interview Copilot', description: 'Description for Project 3...' },
		{ id: 4, name: 'AI Language Tutor', description: 'Description for Project 4...' }
	];
	let disabled = false;
	let data = projects[selectedProject];

	function openModal() {
		data = projects[selectedProject - 1];
		isModalOpen = true;
	}
	onMount(() => {
		function handleKeyPress(event) {
			const key = event.key.toLowerCase();

			if (key === 'j' && selectedProject < projects.length && !disabled) {
				selectedProject++;
			} else if (key === 'k' && selectedProject > 1 && !disabled) {
				selectedProject--;
			} else if (key === 'enter') {
				openModal();
			} else if (key == -'escape') {
				isModalOpen = false;
			} else if (key === 'escape') {
				isModalOpen = false;
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
	<title>projects</title>
	<meta name="description" content="my projects" />
</svelte:head>

<section>
	<p>
		The following list of projects were made in my spare time or during my time at UIUC in various
		courses. Projects include both hardware and software. Click a project to get an expanded view,
		or figure out a different way to navigate ;)
	</p>
	{#each projects as project}
		<div
			class:selected={selectedProject === project.id}
			on:click={() => openModal()}
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
</section>

{#if isModalOpen}
	<NoteModal {closeModal} {data} />
{/if}

<style>
	section {
		height: 300px;
	}

	.selected {
		background: rgba(256, 256, 256, 0.1);
	}

	div:hover {
		background: rgba(256, 256, 256, 0.1);
	}
</style>
