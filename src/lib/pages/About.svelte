<script lang="ts">
import Page from '$lib/components/Page.svelte';
import { baseURL, primaryBackground } from '$lib/utils/constants';
import { onMount } from 'svelte';

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

export let backgroundClass = primaryBackground;

</script>

<svelte:head>
	<title>About</title>
</svelte:head>

<Page id="about" title="About" {backgroundClass}>
	{#if resume_url}
		<!-- svelte-ignore a11y-missing-attribute -->
		<iframe
			src={resume_url}
			class=" h-screen w-screen overscroll-y-auto"
			allow="autoplay"
			scrolling="no"
		/>
	{/if}
</Page>
