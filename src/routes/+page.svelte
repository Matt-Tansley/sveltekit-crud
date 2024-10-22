<script lang="ts">
	import { onMount } from 'svelte';
	import Table from '$lib/components/Table.svelte';
	import Dialog from '$lib/components/Dialog.svelte';

	type Post = {
		createdAt: Date;
		image: any;
		content: string;
		title: string;
		id: number;
	};

	let items: Post[] = [];
	let loaded = true;
	let showModal: boolean = false;

	onMount(() => loadThings(false));

	function loadThings(wait: boolean) {
		if (typeof fetch !== 'undefined') {
			loaded = false;

			fetch('https://api.fake-rest.refine.dev/posts')
				.then((response) => response.json())
				.then((json) =>
					setTimeout(
						() => {
							items = json;
							loaded = true;
						},
						// Simulate a long load time.
						wait ? 2000 : 0
					)
				);
		}
	}
</script>

{#if !loaded}
	<div class="container fully-center">
		<progress></progress>
	</div>
{:else}
	<main class="container">
		<button on:click={() => (showModal = true)}>Add New</button>

		<Table {items} />

		<Dialog bind:showModal />
	</main>
{/if}
