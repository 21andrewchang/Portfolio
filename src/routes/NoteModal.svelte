<script>
	export let closeModal;
	export let data;

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
		<div class="header">
			<p style="font-weight: 600">{data.name}</p>
			<p style="color: rgba(256,256,256, 0.2)">{data.date ? data.date : ''}</p>
		</div>

		<p>{data.description}</p>
	</div>
</div>

<style>
	.header {
		flex-direction: row;
		display: flex;
		justify-content: space-between;
	}
	.modal {
		position: fixed;
		top: 0;
		left: 0;
		background: rgba(0, 0, 0, 0.8);
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
		backdrop-filter: blur(1px);
	}

	.modal-content {
		border: 1px solid rgba(26, 26, 26);
		padding-left: 20px;
		padding-right: 20px;
		width: 600px;
		height: 280px;
		overflow: auto;
		background: rgba(0, 0, 0, 0.95);
	}
</style>
