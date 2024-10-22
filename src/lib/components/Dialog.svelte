<script lang="ts">
	// @ts-nocheck
	let title = '';
	let content = '';

	let dialog: HTMLDialogElement;
	export let showModal = false;

	$: if (showModal) dialog.showModal();

	function close() {
		dialog.close();
		showModal = false;
	}

	function handleSubmit(event: Event) {
		event.preventDefault();
		// Handle form submission (createPost logic would go here)
	}

	async function createPost() {
		console.log('Creating post');

		const res = await fetch(`https://api.fake-rest.refine.dev/posts`, {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({
				title,
				content,
				createdAt: Date.now()
			})
		}).then((res) => {
			res.json();
			close();
		});
	}
</script>

<dialog bind:this={dialog} aria-labelledby="list-title" aria-describedby="list-content">
	<article>
		<h2 id="list-title">Create New Post</h2>
		<div id="mandatory-content">
			<form on:submit={handleSubmit}>
				<div>
					<label for="title">Title</label>
					<input type="text" id="title" bind:value={title} required />
				</div>
				<div>
					<label for="content">Content</label>
					<textarea id="content" bind:value={content} maxlength="2500" required></textarea>
					<small>{content.length} / 2500</small>
				</div>
			</form>
		</div>
		<footer>
			<button on:click={createPost}>Create</button>
			<button on:click={close}>Close</button>
		</footer>
	</article>
</dialog>
