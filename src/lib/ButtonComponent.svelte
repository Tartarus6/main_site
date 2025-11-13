<script lang="ts">
	import type { Snippet } from "svelte";

	interface Props {
		button?: boolean;
		fitContainerHeight?: boolean;
		class?: string;
		children?: Snippet;
	}

	let props: Props = $props();
</script>

<div class="{props.class} wrapper text-tarred-100 grid {props.fitContainerHeight ? 'h-full' : 'h-fit'} grid-cols-1 grid-rows-1 p-2">
	<div class="face p-2 {props.button ? 'select-none' : 'no-press'}">
		{#if props.children}
			{@render props.children()}
		{/if}
	</div>
	<div class="shadow"></div>
</div>
