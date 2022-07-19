<script lang="ts">

import Page from "$lib/components/Page.svelte";
import { baseURL, primaryBackground } from "$lib/utils/constants";
import { onMount } from "svelte";

var portfolio_projects:any[] = [];
var portfolio_personal_projects: any[] = [];

async function loadProjects() {
  await fetch(baseURL+`/project/`, {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json'
    }
  })
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
      portfolio_projects = data;
    });
}

async function loadPersonalProjects() {
  await fetch(baseURL+`/project/get_personal_projects`, {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json'
    }
  })
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
      portfolio_personal_projects = data["projects"];
    });
}

onMount(async () => {
  loadProjects();
  loadPersonalProjects();
});

export let backgroundClass = primaryBackground;

</script>

<svelte:head>
	<title>Projects</title>
</svelte:head>


<Page id="projects" title="Projects" {backgroundClass}>
	<div class="container px-4 flex-grow w-full py-4 sm:py-16 mx-auto px-0">
    <div class="mx-auto w-full md:w-4/5 px-4">
      <div class="container my-8">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-3xl">
            Personal Projects
          </h2>
          <div>
          </div>
        </div>
        <div
          id="scrollContainer"
          class="flex flex-no-wrap overflow-x-scroll scrolling-touch items-start mb-8"
        >
          {#each portfolio_personal_projects as project}
            <div
              class="flex-none w-2/3 md:w-1/3 mr-8 md:pb-4 border rounded-lg"
            >
              <a href="{project.link}" target="_blank" class="space-y-4">
                <div class="aspect-w-16 aspect-h-9">
                  <img
                    class="object-cover shadow-md hover:shadow-xl rounded-lg"
                    src="{project.image_url}"
                    alt=""
                  />
                </div>
                <div class="px-4 py-2">
                  <div class="text-lg leading-6 font-medium space-y-1 truncate">
                    <h3 class="font-bold text-gray-800 text-lg mb-2">
                      {project.name.replace(new RegExp('-', 'g'), " ")}
                    </h3>
                  </div>
                  <div class="m-1">
                    {#each project.languages as language}

                      <button class="{language} text-xs m-1 bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow">
                        {language}
                      </button>
                    {/each}
                  </div>
                  <div class="text-lg">
                    <p class="">
                      {project.description}
                    </p>
                    <p class="font-medium text-sm text-indigo-600 mt-2">
                      Read more<span class="text-indigo-600">&hellip;</span>
                    </p>
                    <p class="font-medium text-sm text-indigo-600 mt-2">
                      <a href="{project.link}" target="_blank">Github repository</a>
                    </p>
                  </div>
                </div>
              </a>
            </div>
          {/each}
        </div>
      </div>
      <!---->
      <div class="container my-8">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-3xl font-medium">
            Other projects
          </h2>
          <div>
          </div>
        </div>
        <div
          id="scrollContainer"
          class="flex flex-no-wrap overflow-x-scroll scrolling-touch items-start mb-8"
        >

          {#each portfolio_projects as project}
            <div
              class="flex-none w-2/3 md:w-1/3 mr-8 md:pb-4 border rounded-lg"
            >
              <a href="{project.url}" class="space-y-4" target="_blank">
                <div class="aspect-w-16 aspect-h-9">
                  <img
                    class="object-cover shadow-md hover:shadow-xl rounded-lg"
                    src="{project.image_url}"
                    alt=""
                  />
                </div>
                <div class="px-4 py-2">
                  <div class="text-lg leading-6 font-medium space-y-1">
                    <h3 class="font-bold text-gray-800 text-3xl mb-2">
                      {project.name}
                    </h3>
                  </div>
                  <div class="m-1">
                    {#each project.languages.data as language}

                      <button class="{language} text-xs m-1 bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow">
                        {language}
                      </button>
                    {/each}
                  </div>
                  <div class="text-lg">
                    <p class="">
                      {project.description}
                    </p>
                    <p class="font-medium text-sm text-indigo-600 mt-2">
                      Read more<span class="text-indigo-600">&hellip;</span>
                    </p>
                  </div>
                </div>
              </a>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</Page>


<style>
  .Arduino { color: #bd79d1; }
  .Assembly { color: #6E4C13; }
  .C-Sharp { color: #178600; }
  .Clojure { color: #db5855; }
  .cpp { color: #f34b7d; }
  .FORTRAN { color: #4d41b1; }
  .HTML { color: #e44b23; }
  .Java { color: #b07219; }
  .JavaScript { color: #f1e05a; }
  .Julia { color: #a270ba; }
  .Jupyter-Notebook { color: #DA5B0B; }
  .Kotlin { color: #F18E33; }
  .Makefile { color: #427819; }
  .Matlab { color: #bb92ac; }
  .Perl { color: #0298c3; }
  .Python { color: #3572A5; }
  .R { color: #198ce7; }
  .Ruby { color: #701516; }
  .Rust { color: #dea584; }
  .Swift { color: #ffac45; }
  .TypeScript { color: #2b7489; }
  .Unity3D-Asset { color: #ab69a1; }
  .Vue { color: #2c3e50; }
</style>