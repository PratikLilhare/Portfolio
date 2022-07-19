<script lang="ts">

import Page from "$lib/components/Page.svelte";
import { baseURL, primaryBackground } from "$lib/utils/constants";
import { onMount } from "svelte";

var skills:any[] = [];

async function loadSkills() {
  await fetch(baseURL+`/user/skill/`, {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json'
    }
  })
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
      skills = data;
    });
}

onMount(async () => {
    loadSkills();
});

export let backgroundClass = primaryBackground;

</script>


<svelte:head>
	<title>Skills</title>
</svelte:head>



<Page id="skills" title="Skills" {backgroundClass}>
    <div class="container px-4 flex-grow w-2/3 py-4 sm:py-16 mx-auto px-0 text-center">
        <span class="inline-flex space-x-3 font-medium">
            <li class="text-[#69a8dc]">
                Backend
            </li>
            <li class="text-[#5ad99c]">
                DevOps
            </li>
            <li class="text-[#dd9288]">
                Frontend
            </li>
            <li class="text-[#b179e6]">
                Other
            </li>
        </span>
        <div class="p-5">
            {#each skills as skill}
                <button 
                    class=
                        "{skill.type} text-white font-bold py-2 px-4 
                        rounded-full m-2"
                    disabled
                    >
                    {skill.name}
                </button>
            {/each}
        </div>
    </div>
</Page>

<style>
    .BACKEND { background-color: #69a8dc; }
    .DEVOPS { background-color: #5ad99c; }
    .FRONTEND { background-color: #dd9288; }
    .OTHER { background-color: #b179e6; }

    /* .OTHER { background-color: #f3f3f3; } */
</style>