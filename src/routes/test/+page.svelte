<script lang="ts">
	let showModal: boolean = false;
	let dialog: HTMLDialogElement;

	$: if (showModal) dialog.showModal(); // Make this reactive, so show will trigger when it is set to true

	function close() {
		dialog.close();
		showModal = false;
	}
</script>

<h1>We are now outside of the modal</h1>
<button on:click={() => dialog.showModal()}>Open Modal</button>

<dialog bind:this={dialog}>
	<article>
		<h1>Modal</h1>
		<footer>
			<button on:click={close}>Close</button>
		</footer>
	</article>
</dialog>
