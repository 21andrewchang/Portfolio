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
			date: 'dec 10 23',
			name: 'Journal entry 2',
			description: 'journal 2 stuff and other stuff and this and that lol'
		},
		{
			id: 2,
			date: 'nov 10 23',
			name: 'Journal entry 1',
			description: 'journal 1 stuff and other stuff and this and that lol'
		},
		{
			id: 3,
			date: 'jul 10 23',
			name: 'Thoughts on stuff',
			description: 'stuff is very stuff and i think a this and that about that and this'
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
	<title>thoughts</title>
	<meta name="description" content="thoughts" />
</svelte:head>

<section>
	<p>a list of kind semi-organized thoughts</p>
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
