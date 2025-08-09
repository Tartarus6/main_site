<script lang="ts">
	import ButtonComponent from './ButtonComponent.svelte';

	interface Props {
		children: () => any;
		flipped: string;
		title: string;
		content: string;
		href: string;
	}

	let { children, flipped = 'false', title = '', content = '', href }: Props = $props();
</script>

<div class="card-component">
	<a {href}>
		<ButtonComponent button="true">
			<div
				class="grid w-full {flipped === 'true'
					? 'grid-cols-[1fr_auto] place-content-end'
					: 'grid-cols-[auto_1fr] place-content-end'}"
			>
				<div
					class="icon-container row-start-1 size-36 place-self-center p-2 max-[30rem]:hidden {flipped ===
					'true'
						? 'col-start-2 ml-4'
						: 'col-start-1 mr-4'}"
				>
					<div class="h-full w-full overflow-hidden">
						{@render children()}
					</div>
				</div>
				<div
					class="row-start-1 grid grid-rows-[auto_auto] place-content-start {flipped === 'true'
						? 'col-start-1 justify-end'
						: 'col-start-2'}"
				>
					<span class="mb-2 text-[1.5em] font-extrabold {flipped === 'true' ? 'text-right' : ''}"
						>{title}</span
					>
					<span class="text-lg {flipped === 'true' ? 'text-right' : ''}">{content}</span>
				</div>
			</div>
		</ButtonComponent>
	</a>
</div>

<style>
	.icon-container {
		background: var(--color-tarblue-800);
		border-radius: 0.5em;
	}

	.icon-container :global(svg) {
		width: 100%;
		height: 100%;
	}

	.icon-container :global(svg .s0) {
		fill: var(--color-tarblue-500);
	}
	.icon-container :global(svg .s1) {
		fill: var(--color-tarblue-200);
	}
	.icon-container :global(svg .s2) {
		fill: var(--color-tarblue-700);
	}
	.icon-container :global(svg .s3) {
		fill: var(--color-tarblue-400);
	}
	.icon-container :global(svg .s4) {
		fill: var(--color-tarblue-600);
	}
	.icon-container :global(svg .c0) {
		stroke: var(--color-tarblue-200);
	}
</style>
