<script lang="ts">
	import Anchor from './Anchor.svelte';

	export let id: string;
	export let title: string = '';
	export let backgroundClass: string = 'bg-neutral-200 dark:bg-neutral-900';
</script>

<Anchor {id} />
<div class="flex flex-col items-center page {backgroundClass}mb-5">
	<div class="pt-4 pb-2 text-4xl text-center">{title}</div>
	<slot />
</div>

<style global>
	.page {
		min-height: calc(100vh - 4rem);
		width: 100%;
	}
</style>
