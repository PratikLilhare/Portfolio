<script lang="ts">
import Page from '$lib/components/Page.svelte';
import { baseURL, primaryBackground } from '$lib/utils/constants';
import { createEventDispatcher, onMount } from 'svelte';

let resume_url = '';
async function loadResume() {
	await fetch(baseURL+`/resume/url/`, {
		method: 'GET',
		headers: {
			'Content-Type': 'application/json'
		}
	})
		.then((response) => response.json())
		.then((data) => {
			resume_url = data.data.url;
		});
}

onMount(async () => {
	loadResume();
});

let showResume = false;
let dispatch = createEventDispatcher();
export function show() {
	showResume = !showResume;
	dispatch('show', showResume);
	}

export let backgroundClass = primaryBackground;

</script>

<svelte:head>
	<title>About</title>
</svelte:head>

<Page id="about" title="About" {backgroundClass}>
	{#if showResume}
		<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded m-2" on:click={show}>
			Hide
		</button>
		{#if resume_url}
			<!-- svelte-ignore a11y-missing-attribute -->
			<iframe
				src={resume_url}
				class=" h-screen lg:w-2/4 sm:w-screen overscroll-y-auto"
				allow="autoplay"
				scrolling="no"
			/>
		{/if}
	{:else}
		<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded m-2" on:click={show}>
			Show resume
		</button>
	{/if}
</Page>
