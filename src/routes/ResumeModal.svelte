<script>
	export let closeModal;
	import { onMount } from 'svelte';

	onMount(() => {
		const modalElement = document.getElementById('modal');

		if (modalElement) {
			modalElement.addEventListener('click', function () {
				closeModal();
			});
		}

		const iframe = modalElement.querySelector('iframe');

		iframe.addEventListener('error', (event) => {
			console.error('Error loading PDF:', event);
		});
	});
</script>

<div class="modal" id="modal">
	<div class="modal-content">
		<iframe src="../lib/resume.pdf" title="resume" frameborder="0"></iframe>
	</div>
</div>

<style>
	.modal {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.5);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
	}

	.modal-content {
		background-color: #fff;
		padding: 20px;
		max-width: 80%;
		max-height: 80%;
		overflow: auto;
	}

	iframe {
		width: 100%;
		height: 100%;
	}
</style>
