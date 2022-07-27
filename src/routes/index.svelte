<script lang="ts">
import About from '$lib/pages/About.svelte';
import Experience from '$lib/pages/Experience.svelte';
import Home from '$lib/pages/Home.svelte';
import Projects from '$lib/pages/Projects.svelte';
import Skills from '$lib/pages/Skills.svelte';
import { primaryBackground } from '$lib/utils/constants';
</script>

<svelte:head>
	<title>Pratik Lilhare</title>
</svelte:head>

<main class="grid grid-cols-1 divide-y-2 p-5 space-y-[10vh] {primaryBackground}">
	<section id="home">
		<Home />
	</section>

	<section id="about">
		<About />
	</section>

	<section id="experience">
		<Experience />
	</section>

	<section id="skills">
		<Skills />
	</section>

	<section id="projects">
		<Projects />
	</section>
</main>

<style>
	section {
		min-height: 100vh;
	}
</style>
