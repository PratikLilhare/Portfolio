<script lang="ts">
import { primaryBackground } from '$lib/utils/constants';
import Anchor from './Anchor.svelte';
export let id: string;
export let title: string = '';
</script>

<Anchor {id} />
<div class="flex flex-col items-center page {primaryBackground} mt-5 sm:text-sm lg:text-lg md:text-md">
	<div class="pt-4 pb-2 text-4xl text-center underline">{title}</div>
	<slot />
</div>

<style global>
	.page {
		min-height: calc(100vh - 4rem);
		width: 100%;
	}
</style>
