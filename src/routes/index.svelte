<script lang="ts">
	import Navbar from '$lib/components/Navbar.svelte';

	import About from '$lib/pages/About.svelte';
	import Home from '$lib/pages/Home.svelte';
	import Projects from '$lib/pages/Projects.svelte';
</script>

<main class="grid grid-cols-1 divide-y-2 p-5 space-y-4">
	<section id="home">
		<Home />
	</section>

	<section id="about">
		<About />
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
