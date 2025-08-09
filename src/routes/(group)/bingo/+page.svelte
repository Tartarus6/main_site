<script lang="ts">
	import BingoComponent from '$lib/BingoComponent.svelte';

	import type { PageData } from './$types';

	let { data }: { data: PageData } = $props();
</script>

<div class="grid place-items-center">
	<BingoComponent items={data.items}></BingoComponent>
</div>
