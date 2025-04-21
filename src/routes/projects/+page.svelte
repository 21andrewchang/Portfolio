<script>
	//bug where if you hover and use j and k to move theres two highlights
	import { onMount } from 'svelte';
	import NoteModal from '../../lib/components/NoteModal.svelte';

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
			description: [
				'- Developed Tetris game using SystemVerilog and ran on an FPGA board.',
				'- Utilized a matrix-based approach for Tetrimino positioning.',
				'- Implemented block movement, rotation, collision detection, and line clearing logic.',
				'- Integrated FPGA board with VGA interface for real-time display on monitor.',
				'- Implemented keyboard control mapping for Tetrimino movement.'
			]
		},

		{
			id: 2,
			date: 'wnt 23',
			name: 'Voltage Regulated AC-DC Power Supply',
			description: [
				'- Main circuit components: zener diodes, op-amps, transistors (BJT)',
				'- Designed and tested circuit on LTSpice',
				'- Initial testing on breadboard then soldered to PCB',
				'- Tested using transformer and signal generator',
				'- Project provided insights into circuit design, soldering, and power supply efficiency.'
			]
		},

		{
			id: 3,
			date: 'wnt 23',
			name: 'LeNet-5 Convolutional Layer Optimization',
			description: [
				'- Enhanced LeNet-5 convolutional layer using CUDA for image classification',
				'- Developed and optimized GPU convolution kernel for various dataset sizes',
				'- Optimized GPU kernel: tiling/shared memory, FP16, Streams, input unrolling',
				'- Utilized Nsight tools for in-depth performance analysis and gprof for profiling',
				'- Gave insights to CUDA, performance optimization, and GPU programming'
			]
		},
		{
			id: 4,
			date: 'sum 23',
			name: 'Interview Copilot',
			description: 'Description for Project 3...'
		},
		{
			id: 5,
			date: 'fal 23',
			name: 'AI Language Tutor',
			description: 'Description for Project 4...'
		},
		{
			id: 6,
			date: 'sum 23',
			name: 'Twitter Clone',
			description: [
				'- Developed Twitter Clone to learn web development.',
				'- Basic functionality for posting messages and user management.',
				'- Used PlanetScale for message storage, Drizzle ORM, and Clerk for authentication.',
				'- Organized users and posts in the database, enabling profile views of individual user posts.',
				'- Gave insight towards web development database design and tech stacks'
			]
		}
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
