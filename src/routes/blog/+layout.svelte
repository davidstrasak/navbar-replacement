<script lang="ts">
	import "../../app.css";
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { base } from "$app/paths";
	import { page } from "$app/state";

	let isOpen = false;
	let y:number;
	let fadeIn: string = "fade-in"; // This holds the "fade-in" class for the button
  
	function toggleMenu() {
	  isOpen = !isOpen;
	}

	//BLOCK 5 - Typewriter effect for the name
	let typewriter: string;
	typewriter = "typewriter";
	onMount(() => {
		setTimeout(() => {
			typewriter = "vanillaTypewriter";
		}, 2000);

		setTimeout(() => {
			// This removes the fade-in class from the button after 2 seconds, because otherwise it would fade on click
			fadeIn = "";
		}, 2000);
	});
  </script>
  
  <svelte:window bind:scrollY={y}/>
  
  <div class="min-h-screen font-primary">
	<header class="fixed top-0 left-0 right-0 z-50 bg-base-100 shadow-md transition-all duration-300 font-systemancer" class:shadow-lg={y > 0}>
	  <nav class="container mx-auto px-4 py-4">
		<div class="mx-auto w-full md:w-4/5 lg:w-3/5 flex justify-between items-center">
			<button class="btn btn-ghost text-2xl lg:btn-lg lg:text-3xl inline ">
				{#key page.url.pathname}
					<a href={`${base}/`} class="inline">
						<div class={typewriter}>SYSTEMANCER</div>
					</a>
				{/key}
			</button>

		  
		  <div class="hidden md:flex space-x-4 {fadeIn}">
				{#key page.url.pathname}
					<a href={`${base}/blog`} class="btn btn-ghost xl:btn-lg text-xl xl:text-2xl"> Blog </a>
				{/key}
				{#key page.url.pathname}
					<a href={`${base}/projects`} class="btn btn-ghost xl:btn-lg text-xl xl:text-2xl"> Projects </a>
				{/key}
				{#key page.url.pathname}
					<a href={`${base}/CV`}  class="btn btn-ghost xl:btn-lg text-xl xl:text-2xl"> CV </a>
				{/key}
		  </div>
		  
		  <button
						class="inline {fadeIn} md:hidden"
						on:click={() => {
							toggleMenu();
						}}
						aria-label="Toggle navigation menu"
						><svg
							fill="#00ff00"
							clip-rule="evenodd"
							fill-rule="evenodd"
							stroke-linejoin="round"
							stroke-miterlimit="2"
							viewBox="0 0 24 24"
							xmlns="http://www.w3.org/2000/svg"
							height="50"
							width="50"
							><path
								d="m21 17.75c0-.414-.336-.75-.75-.75h-16.5c-.414 0-.75.336-.75.75s.336.75.75.75h16.5c.414 0 .75-.336.75-.75zm0-4c0-.414-.336-.75-.75-.75h-16.5c-.414 0-.75.336-.75.75s.336.75.75.75h16.5c.414 0 .75-.336.75-.75zm0-4c0-.414-.336-.75-.75-.75h-16.5c-.414 0-.75.336-.75.75s.336.75.75.75h16.5c.414 0 .75-.336.75-.75zm0-4c0-.414-.336-.75-.75-.75h-16.5c-.414 0-.75.336-.75.75s.336.75.75.75h16.5c.414 0 .75-.336.75-.75z"
								fill-rule="nonzero"
							/></svg
						></button
					>
		</div>
	  </nav>
	  
	  {#if isOpen}
		<div class="md:hidden" transition:fly="{{ y: -200, duration: 300 }}">
		  <div class="mx-auto w-full md:w-4/5 lg:w-3/5">
				{#key page.url.pathname}
					<a href={`${base}/blog`} class="block py-2 px-4 text-sm hover:bg-gray-700 w-full text-left"> Blog </a>
				{/key}
				{#key page.url.pathname}
					<a href={`${base}/projects`} class="block py-2 px-4 text-sm hover:bg-gray-700 w-full text-left" > Projects </a>
				{/key}
				{#key page.url.pathname}
					<a href={`${base}/CV`} class="block py-2 px-4 text-sm hover:bg-gray-700 w-full text-left"> CV </a>
				{/key}
		  </div>
		</div>
	  {/if}
	</header>
  
	<main class="container mx-auto px-4 pt-20 lg:pt-24 font-primary fade-in">
	  <div class="mx-auto w-full md:w-4/5 lg:w-3/5 bg-base-100 p-6 shadow-lg">
		<slot />
	  </div>
	</main>
  </div>
  