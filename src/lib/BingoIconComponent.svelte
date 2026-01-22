<script lang="ts">
	import ButtonComponent from './ButtonComponent.svelte';

	interface Props {
		boardSize?: number,     // width/height of the board
		interactive?: boolean,  // whether hovering on the cells will toggle them
		boardState?: boolean[], // n^2 length array setting the filled (true) and un-filled (false) values in the board (the value is ignored in the free space)
		boardText?: string[],   // n^2 length array setting the text in each cell of the board (the text in the free space is ignored)
	}

	let { boardSize = 5, interactive = true, boardState, boardText }: Props = $props();

	// let scaleFactor = $state(1);
	let board: HTMLDivElement;
	let selected: boolean[] = $state(Array(boardSize * boardSize).fill(false));
	let text: string[] = $state(Array(boardSize * boardSize).fill(""));

	// applying boardState
	if (boardState && boardState.length == selected.length) {
		selected = boardState;
	}

	// applying boardText
	if (boardText && boardText.length == text.length) {
		text = boardText;
	}

	const centerIndex = Math.floor((boardSize * boardSize) / 2);

	selected[centerIndex] = true;

	function toggleSelected(index: number) {
		if (index !== centerIndex) {
			selected[index] = !selected[index];
		}
	}
</script>

<!-- Note: size of 384 is equivalent to tailwind 'size-96' -->
<svg viewBox="0 0 384 384" class="w-full h-full">
	<foreignObject class="size-96">
		<div
			bind:this={board}
			class="relative grid w-full h-full origin-top-left"
			style="grid-template-columns: repeat({boardSize}, 1fr); transform: translate(calc(var(--thickness) / 2), calc(var(--thickness) / 2))"
		>
		{#each Array(boardSize * boardSize) as _, index}
			<button onmouseenter={() => {if (interactive) toggleSelected(index)}}>
				<ButtonComponent
					button={true}
					fitContainerHeight={true}
					class={index === centerIndex
						? 'center selected'
						: selected[index]
							? 'bingo selected'
							: 'bingo'}
				>
					<div class="absolute inset-0 grid place-items-center text-center text-3xl pointer-events-none">
						{#if text[index]}
							<span class="px-2">{text[index]}</span>
						{:else}
							<span class="text-transparent">.</span>
						{/if}
					</div>
				</ButtonComponent>
			</button>
		{/each}
	</div>
	</foreignObject>
</svg>

<style>
	:global(.bingo div.face:hover:not(:active), .bingo div.face:hover.no-press) {
		--thickness: 0.3em;
	}
</style>
