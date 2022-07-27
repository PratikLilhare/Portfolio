<script lang="ts">
import { neutralBackground } from "$lib/utils/constants";


let m = new Map();
m.set('Home', '#home');
m.set('About', '#about');
m.set('Experience', '#experience');
m.set('Skills', '#skills');
m.set('Projects', '#projects');

function scrollIntoView({ target }: { target: any }) {
	const el = document.querySelector(target.getAttribute('href'));

	if (!el) return;
	el.scrollIntoView({
		behavior: 'smooth',
		block: 'start'
	});
}

async function toggle_theme() {
	console.log('theme')
	document.documentElement.classList.toggle('dark')
	localStorage.setItem('theme', localStorage.theme === 'dark'?'white':'dark')
}
</script>

<nav class="flow-root flex bg-white sticky top-0 z-50 h-[var(--header-height)] border-b-2 {neutralBackground}">
	<hr/><hr/>
	<a href="/" class="float-left px-3 py-2 text-slate-700 dark:text-white font-bold">Portfolio</a>

	<div class="float-right mx-2">

		<div class="dropdown inline-block relative">
		  <button class="bg-gray-400 font-semibold py-2 px-4 rounded inline-flex items-center dark:bg-gray-800 dark:text-white">
			<span class="mr-1">Menu</span>
			<svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/> </svg>
		  </button>
		  <ul class="dropdown-menu absolute hidden text-gray-700 pt-1">
			{#each [...m] as [title, url]}
				<li>
					<a
						href={url}
						class="rounded-l-full m-1 bg-gray-400  float-right px-3 py-2 text-slate-700 font-medium hover:bg-slate-200 hover:text-slate-900 dark:bg-gray-300 dark:text-slate-700  dark:hover:bg-slate-200 dark:hover:text-slate-900"
						on:click|preventDefault={scrollIntoView}
					>
						{title}
					</a>
				</li>
			{/each}
		  </ul>
		</div>
	  
	</div>

	<!-- Dark mode button -->
	<button 
		title="Toggle Theme" 
		on:click={toggle_theme}
		class="
		mt-2
			float-right
			w-12 
			h-6 
			rounded-full 
			p-1 
			bg-gray-400 
			dark:bg-gray-600 
			relative 
			transition-colors 
			duration-500 
			ease-in
			focus:outline-none 
			focus:ring-2 
			focus:ring-blue-700 
			dark:focus:ring-blue-600 
			focus:border-transparent
		">
		<div id="toggle"
			class="
				rounded-full 
				w-4 
				h-4 
				bg-blue-600 
				dark:bg-blue-500 
				relative 
				ml-0 
				dark:ml-6 
				pointer-events-none 
				transition-all 
				duration-300 
				ease-out
			">
		</div>
	</button>
	<!-- Dark mode button end -->
</nav>

<style>
	.dropdown:hover .dropdown-menu {
  		display: block;
	}
</style>