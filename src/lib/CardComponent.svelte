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
		<ButtonComponent button={true}>
			<div class="card-content w-full">
				<div
					class="icon-container size-36 p-2 max-[30rem]:size-28 {flipped === 'true'
						? 'float-right ml-4'
						: 'float-left mr-4'}"
				>
					<div class="h-full w-full overflow-hidden">
						{@render children()}
					</div>
				</div>
				<div class="content-text">
					<h3 class="mb-2 text-[1.5em] font-extrabold {flipped === 'true' ? 'text-right' : ''}">
						{title}
					</h3>
					<p class="text-lg {flipped === 'true' ? 'text-right' : ''}">{content}</p>
				</div>
			</div>
		</ButtonComponent>
	</a>
</div>

<style>
	.card-content {
		overflow: hidden; /* Clears float containment */
	}

	.icon-container {
		background: var(--color-tarblue-800);
		border-radius: 0.5em;
		shape-outside: margin-box; /* Improves text wrapping around the floated element */
	}

	.content-text h3 {
		clear: none; /* Allows title to wrap around icon */
	}

	.content-text p {
		clear: none; /* Allows paragraph to wrap around icon */
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
