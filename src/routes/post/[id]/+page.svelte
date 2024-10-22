<script>
	import { goto } from '$app/navigation';

	export let data;

	let valueA = data.title;
	let value = data.content;

	async function editPost() {
		const res = await fetch(`https://api.fake-rest.refine.dev/posts/${data.id}`, {
			method: 'PATCH',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({
				title: valueA,
				content: value
			})
		}).then((res) => {
			res.json();
			goto('/');
		});
	}
</script>

<body class="container">
	<main>
		<article>
			<div>
				<label for="title">Edit Title</label>
				<input type="text" id="title" bind:value={valueA} />
			</div>
			<div>
				<label for="content">Edit Content</label>
				<textarea id="content" bind:value maxlength="2500"></textarea>
				<small>{value.length} / 2500</small>
			</div>
		</article>
	</main>
	<footer>
		<button on:click={editPost}>Edit</button>
	</footer>
</body>
