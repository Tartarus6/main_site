<script lang="ts">
	import ButtonComponent from './ButtonComponent.svelte';
	import type { Snippet } from 'svelte';

	interface Props {
		title: string;
		children?: Snippet;
	}

	let { title, children }: Props = $props();
</script>

<div class="terminal-component w-full pb-2">
	<ButtonComponent>
		<div class="grid w-full grid-cols-1">
			<div class="mb-2 grid grid-cols-[auto_1fr]">
				<span class="mr-6 text-xl font-extrabold select-none">>_</span>
				<span class="text-lg">{title}</span>
			</div>
			<div class="bg-tarblue-800 terminal-component-content w-full rounded-2xl p-2">
				{#if children}
					{@render children()}
				{/if}
			</div>
		</div>
	</ButtonComponent>
</div>

<!-- This is how the component can be styled to maintain terminal-like formatting -->
<style>
	:global(.terminal-component-content > *) {
		display: grid;
		grid-template-columns: auto 1fr;
		margin: 0;
	}

	:global(.terminal-component-content > *::before) {
		all: unset;
		content: '>';
		margin-right: 0.5rem;
		font-weight: bold;
		color: rgb(34 197 94); /* text-green-500 */
		user-select: none;
		font-size: 1rem; /* Standard fixed font size */
		display: flex;
		align-items: center; /* Vertically center the prefix */
		text-decoration: none; /* Prevent underline or other decorations */
	}

	:global(.terminal-component-content *) {
		color: var(--color-tarblue-100, #e2e8f0);
	}
</style>
