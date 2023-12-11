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
			date: 'spr 23',
			name: 'FPGA Tetris',
			description:
				'I developed a Tetris game using SystemVerilog on an FPGA board. The game utilized a matrix-based approach to manage Tetrimino positioning and used clock cycles on the FPGA to progress the game. I implemented block movement, rotation, collision detection, and line clearing logic. By integrating the FPGA board with a VGA interface, the game was displayed in real-time on an external monitor. Controlling the movement of the Tetrimino was done through keyboard control, where I mapped key inputs to the movement in C. '
		},
		{
			id: 2,
			date: 'wnt 23',
			name: 'LeNet-5 Convolutional Layer Optimization',
			description: 'Description for Project 2...'
		},
		{
			id: 3,
			date: 'sum 23',
			name: 'Interview Copilot',
			description: 'Description for Project 3...'
		},
		{ id: 4, date: 'fa 23', name: 'AI Language Tutor', description: 'Description for Project 4...' }
	];
	let disabled = false;
	let data = projects[selectedProject];

	function toggleModal() {
		data = projects[selectedProject - 1];
		if (isModalOpen) {
			isModalOpen = false;
		} else {
			isModalOpen = true;
		}
	}
	onMount(() => {
		function handleKeyPress(event) {
			const key = event.key.toLowerCase();

			if (key === 'j' && selectedProject < projects.length && !disabled) {
				selectedProject++;
				data = projects[selectedProject - 1];
			} else if (key === 'k' && selectedProject > 1 && !disabled) {
				selectedProject--;
				data = projects[selectedProject - 1];
			} else if (key === 'enter') {
				toggleModal();
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
	<p>a list of projects made at school or in my free time</p>
	{#each projects as project}
		<div
			class:selected={selectedProject === project.id}
			on:click={() => toggleModal()}
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
