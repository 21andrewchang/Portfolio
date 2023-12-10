<script>
	export let closeModal;

	function close() {
		closeModal();
	}
	import { onMount } from 'svelte';

	onMount(() => {
		const modalElement = document.getElementById('modal');

		if (modalElement) {
			modalElement.addEventListener('click', function () {
				close();
			});
		}
	});
</script>

<div class="modal" id="modal">
	<div class="modal-content">
		<p>hello</p>
	</div>
</div>

<style>
	.modal {
		position: fixed;
		top: 0;
		left: 0;
		background: rgba(0, 0, 0, 0.5);
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
	}

	.modal-content {
		padding: 20px;
		max-width: 100%;
		max-height: 100%;
		overflow: auto;
	}

	iframe {
		width: 600px;
		height: 800px;
	}
</style>
