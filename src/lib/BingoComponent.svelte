<script lang="ts">
	import ButtonComponent from './ButtonComponent.svelte';
	import { onMount } from 'svelte';
	import confetti from 'canvas-confetti';

	interface Props {
		items: string[];
	}

	const { items }: Props = $props();

	const boardSize = 5;
	const centerIndex = Math.floor((boardSize * boardSize) / 2);
	let boardTerms: string[] = $state([]);
	let selected: boolean[] = $state(Array(boardSize * boardSize).fill(false));
	let bingoCount = $state(0);
	let previousBingoCount = $state(0);

	// Select the center button by default
	selected[centerIndex] = true;

	let tarblue500: string;
	let tarred500: string;

	onMount(() => {
		tarblue500 = getComputedStyle(document.documentElement).getPropertyValue('--color-tarblue-500');
		tarred500 = getComputedStyle(document.documentElement).getPropertyValue('--color-tarred-500');

		// Shuffle the items array
		const shuffledItems = [...items].sort(() => Math.random() - 0.5);

		// Take the first boardSquares - 1 items for the board (excluding the center)
		boardTerms = shuffledItems.slice(0, boardSize * boardSize - 1);

		// Add a placeholder for the center
		boardTerms.splice(centerIndex, 0, 'FREE');
	});

	function toggleSelected(index: number) {
		if (index !== centerIndex) {
			selected[index] = !selected[index];
			checkBingo(); // Check for bingo after each selection change
		}
	}

	async function checkBingo() {
		let count = 0;

		// Check rows
		for (let i = 0; i < boardSize; i++) {
			let rowBingo = true;
			for (let j = 0; j < boardSize; j++) {
				if (!selected[i * boardSize + j]) {
					rowBingo = false;
					break;
				}
			}
			if (rowBingo) {
				count++;
			}
		}

		// Check columns
		for (let i = 0; i < boardSize; i++) {
			let colBingo = true;
			for (let j = 0; j < boardSize; j++) {
				if (!selected[j * boardSize + i]) {
					colBingo = false;
					break;
				}
			}
			if (colBingo) {
				count++;
			}
		}

		// Check diagonals
		let diag1Bingo = true;
		for (let i = 0; i < boardSize; i++) {
			if (!selected[i * boardSize + i]) {
				diag1Bingo = false;
				break;
			}
		}
		if (diag1Bingo) {
			count++;
		}

		let diag2Bingo = true;
		for (let i = 0; i < boardSize; i++) {
			if (!selected[i * boardSize + (boardSize - 1 - i)]) {
				diag2Bingo = false;
				break;
			}
		}
		if (diag2Bingo) {
			count++;
		}

		if (count > previousBingoCount) {
			await launchConfetti();
		}
		previousBingoCount = count;
		bingoCount = count;
		return count;
	}

	function launchConfetti() {
		return new Promise((resolve) => {
			const confettiCount = 100;

			const defaults = {
				colors: [tarblue500, tarred500]
			};

			function fire(particleRatio: number, opts: any) {
				confetti({
					...defaults,
					...opts,
					particleCount: Math.floor(confettiCount * particleRatio),
					shapes: ['circle']
				});
			}

			fire(0.2, {
				spread: 90,
				angle: 45,
				startVelocity: 55,
				origin: { x: 0, y: 1 }
			});
			fire(0.3, {
				spread: 90,
				angle: 45,
				startVelocity: 35,
				origin: { x: 0, y: 1 }
			});
			fire(0.2, {
				spread: 90,
				angle: 135,
				startVelocity: 55,
				origin: { x: 1, y: 1 }
			});
			fire(0.3, {
				spread: 90,
				angle: 135,
				startVelocity: 35,
				origin: { x: 1, y: 1 }
			});

			resolve(null);
		});
	}
</script>

<span class="text-tarred-100 mb-8 text-6xl">Bingos: {bingoCount}</span>

<div class="grid max-w-[40em]" style="grid-template-columns: repeat({boardSize}, 1fr);">
	{#each Array(boardSize * boardSize) as _, index}
		<button onmousedown={() => toggleSelected(index)} class="aspect-square">
			<ButtonComponent
				button="true"
				fitContainerHeight="true"
				class={index === centerIndex
					? 'center selected'
					: selected[index]
						? 'bingo selected'
						: 'bingo'}
			>
				<div class="grid w-full grid-cols-[1fr]">
					<div class="place-self-center justify-self-center max-[35em]:text-[0.6125em]">
						{boardTerms[index]}
					</div>
				</div>
			</ButtonComponent>
		</button>
	{/each}
</div>
