<script lang="ts">
	export let button = 'false';
	export let fitContainerHeight = 'false';
	let customClass: string = '';

	export { customClass as class };
</script>

<div
	class="{customClass} wrapper text-tarred-100 grid {fitContainerHeight === 'true'
		? 'h-full'
		: 'h-fit'} grid-cols-1 grid-rows-1 p-2"
>
	<div class="face p-2 {button === 'true' ? 'select-none' : 'no-press'}">
		<slot />
	</div>
	<div class="shadow"></div>
</div>
