<script lang="ts">
	export let items: any[] = [];

	async function deletePost(id: number) {
		const res = await fetch(`https://api.fake-rest.refine.dev/posts/${id}`, {
			method: 'DELETE'
		}).then((res) => {
			res.json();
			location.reload();
		});
	}
</script>

<table aria-label="User list" style="width: 100%;">
	<thead>
		<tr>
			<th scope="col">ID</th>
			<th scope="col">Title</th>
			<th scope="col">Date Created</th>
			<th scope="col">Actions</th>
		</tr>
	</thead>
	<tbody>
		{#each items as item, index (index)}
			<tr>
				<td>{item.id}</td>
				<td>{item.title}</td>
				<td>{item.createdAt}</td>
				<td>
					<div role="group">
						<button><a class="link" href={`/post/${item.id}`}>Edit</a></button>
						<button class="contrast" on:click={() => deletePost(item.id)}>Delete</button>
					</div>
				</td>
			</tr>
		{/each}
	</tbody>
</table>

<style>
	.link {
		color: white;
		text-decoration: none;
	}
</style>
