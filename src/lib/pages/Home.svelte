<script>
import Page from "$lib/components/Page.svelte";

import Social from "$lib/components/Social.svelte";
import { baseURL } from "$lib/utils/constants";
import { onMount } from "svelte";

fetch(baseURL+`/test/healthcheck/`, {
	method: 'GET',
	headers: {
		'Content-Type': 'application/json'
	}
});


let avatar_url = '';
async function loadAvatar() {
	await fetch(baseURL+`/user/get_avatar_url/`, {
		method: 'GET',
		headers: {
			'Content-Type': 'application/json'
		}
	})
		.then((response) => response.json())
		.then((data) => {
			avatar_url = data.data.url;
		});
}

onMount(async () => {
	loadAvatar();
});

</script>

<Page id="home" title="">
	<div class="flex flex-col items-center justify-center page">
		<div class="text-center">
				
				
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img 
				class="inline object-cover w-36 h-36 mr-2 rounded-full" 
				src="{avatar_url}"
				alt="profile image" 
			/>
				
			<h1 class="text-4xl m-6">Pratik Lilhare</h1>
			<Social/>

		</div>
		<div class="flex justify-evenly" />
	</div>
</Page>
