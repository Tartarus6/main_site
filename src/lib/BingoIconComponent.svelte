<script lang="ts">
	import { onMount } from 'svelte';
	import ButtonComponent from './ButtonComponent.svelte';

	const boardSize = 5;
	let scaleFactor = $state(1);
	let board: HTMLDivElement;
	let selected: boolean[] = $state(Array(boardSize * boardSize).fill(false));
	const centerIndex = Math.floor((boardSize * boardSize) / 2);

	selected[centerIndex] = true;

	onMount(() => {
		const initialSize = board.clientWidth;
		const container = board.parentElement;
		if (container) {
			const containerWidth = container.clientWidth;
			scaleFactor = containerWidth / initialSize;
		} else {
			console.warn('Bingo board container not found.');
		}
	});

	function toggleSelected(index: number) {
		if (index !== centerIndex) {
			selected[index] = !selected[index];
		}
	}
</script>

<div
	bind:this={board}
	class="relative grid size-96 origin-top-left"
	style="grid-template-columns: repeat({boardSize}, 1fr); scale: {scaleFactor}; transform: translate(calc(var(--thickness) / 2), calc(var(--thickness) / 2))"
>
	{#each Array(boardSize * boardSize) as _, index}
		<button onmouseenter={() => toggleSelected(index)}>
			<ButtonComponent
				button="true"
				fitContainerHeight="true"
				class={index === centerIndex
					? 'center selected'
					: selected[index]
						? 'bingo selected'
						: 'bingo'}
			></ButtonComponent>
		</button>
	{/each}
</div>

<style>
	:global(.bingo div.face:hover:not(:active), .bingo div.face:hover.no-press) {
		--thickness: 0.3em;
	}
</style>
