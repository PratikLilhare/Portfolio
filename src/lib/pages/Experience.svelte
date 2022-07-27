<script lang="ts">

import Page from "$lib/components/Page.svelte";
import { baseURL } from "$lib/utils/constants";
import { onMount } from "svelte";

var experience:any[] = [];

async function loadExperience() {
  await fetch(baseURL+`/user/experience`, {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json'
    }
  })
    .then((response) => response.json())
    .then((data) => {
      experience = data;
    });
}

function stripDate(date = new Date()) {
    const d = date.toLocaleDateString("en-US", {month: "long", year: "numeric"});
    return d
}

onMount(async () => {
    await loadExperience();
});

</script>

<Page id="experience" title="Experience">
    {#each experience as exp}
        <div class="shadow-md rounded-md">

            <div class="p-5 w-full text-sm lg:text-xl">
                <div class="flow-root">
                    <h5 class="float-left font-semibold mb-3">{exp.title}</h5>
                    <p class="float-right">
                        {stripDate(new Date(exp.start))} 
                        - 
                        {#if exp.end}
                            {stripDate(new Date(exp.end))}
                        {:else}
                            Present
                        {/if}
                    </p>
                </div>

                <h5 class="">{exp.company}</h5>

                <main class="w-full p-8 mx-auto">
                    <section class="shadow row">
                        <div class="tabs">
                            <div class="border-b tab">
                                <div class="border-l-2 border-transparent relative">
                                    <input class="w-full absolute z-10 cursor-pointer opacity-0 h-5 top-6" type="checkbox" id="{exp.id}">
                                    <header class="flex justify-between items-center p-5 pl-8 pr-8 cursor-pointer select-none tab-label" for="{exp.id}">
                                        <span class="text-grey-darkest font-thin text-xl">
                                            Description
                                        </span>
                                        <div class="rounded-full border border-grey w-7 h-7 flex items-center justify-center test">
                                            <svg aria-hidden="true" class="" data-reactid="266" fill="none" height="24" stroke="#606F7B" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">
                                                <polyline points="6 9 12 15 18 9">
                                                </polyline>
                                            </svg>
                                        </div>
                                    </header>
                                    <div class="tab-content">
                                        <div class="pl-8 pr-8 pb-5 text-grey-darkest">
                                            {exp.description}
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </section>
                </main>
                
                
                {#each exp.skills as skill}
                    <button 
                        class="text-sm py-2 px-4 rounded shadow m-2"
                        disabled
                        >
                        {skill.name}
                    </button>
                {/each}

    
            </div>
    
        </div>
    {/each}
</Page>


<style>
    .tab {
        overflow: hidden;
    }
    .tab-content {
        max-height: 0;
    }
    input:checked + .tab-label .test svg {
        transform: rotate(180deg);
    }
    input:checked ~ .tab-content {
        max-height: 100vh;
    }
</style>