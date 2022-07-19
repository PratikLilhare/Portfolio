<script lang="ts">
	let m = new Map();
	m.set('Projects', '#projects');
	m.set('Skills', '#skills');
	m.set('About', '#about');
	m.set('Home', '#home');

	function scrollIntoView({ target }: { target: any }) {
		const el = document.querySelector(target.getAttribute('href'));

		if (!el) return;
		el.scrollIntoView({
			behavior: 'smooth',
			block: 'start'
		});
	}
</script>

<nav class="flow-root flex bg-white sticky top-0 z-50 h-[var(--header-height)] border-b-2">
	<hr/><hr/>
	<a href="/" class="float-left px-3 py-2 text-slate-700 font-bold">Portfolio</a>

	{#each [...m] as [title, url]}
		<a
			href={url}
			class="float-right px-3 py-2 text-slate-700 font-medium hover:bg-slate-100 hover:text-slate-900"
			on:click|preventDefault={scrollIntoView}
		>
			{title}
		</a>
	{/each}
</nav>
