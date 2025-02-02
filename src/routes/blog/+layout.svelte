<script lang="ts">
	import "../../app.css";
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { base } from "$app/paths";
  
	let isOpen = false;
	let y:number;
  
	function toggleMenu() {
	  isOpen = !isOpen;
	}
  
	onMount(() => {
	  const mediaQuery = window.matchMedia('(min-width: 768px)');
	  const handleMediaQueryChange = (e: MediaQueryListEvent) => {
		if (e.matches) {
		  isOpen = false;
		}
	  };
	  mediaQuery.addListener(handleMediaQueryChange);
	  return () => mediaQuery.removeListener(handleMediaQueryChange);
	});
  </script>
  
  <svelte:window bind:scrollY={y}/>
  
  <div class="min-h-screen bg-gray-900 text-gray-100 font-systemancer">
	<header class="fixed top-0 left-0 right-0 z-50 bg-gray-800 shadow-md transition-all duration-300" class:shadow-lg={y > 0}>
	  <nav class="container mx-auto px-4 py-4">
		<div class="mx-auto w-full md:w-4/5 lg:w-3/5 flex justify-between items-center">
		  <a href="/" class="text-2xl font-bold text-blue-400">SYSTEMANCER</a>
		  
		  <div class="hidden md:flex space-x-4">
			<a href="/blog" class="text-gray-300 hover:text-blue-400">Blog</a>
			<a href="/project" class="text-gray-300 hover:text-blue-400">Project</a>
			<a href="/CV" class="text-gray-300 hover:text-blue-400">CV</a>
		  </div>
		  
		  <button class="md:hidden text-gray-300" on:click={toggleMenu} aria-label="Toggle menu">
			<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
			  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
			</svg>
		  </button>
		</div>
	  </nav>
	  
	  {#if isOpen}
		<div class="md:hidden" transition:fly="{{ y: -200, duration: 300 }}">
		  <div class="mx-auto w-full md:w-4/5 lg:w-3/5">
			<a href="/blog" class="block py-2 px-4 text-sm text-gray-300 hover:bg-gray-700">Blog</a>
			<a href="/project" class="block py-2 px-4 text-sm text-gray-300 hover:bg-gray-700">Project</a>
			<a href="/CV" class="block py-2 px-4 text-sm text-gray-300 hover:bg-gray-700">CV</a>
		  </div>
		</div>
	  {/if}
	</header>
  
	<main class="container mx-auto px-4 pt-24 font-primary">
	  <div class="mx-auto w-full md:w-4/5 lg:w-3/5 bg-gray-800 p-6 rounded-lg shadow-lg">
		<slot />
	  </div>
	</main>
  </div>
  