<script lang="ts">
	// @ts-nocheck
	import { clickOutside } from "./clickOutside.js";

	export let library_pages: any;
	export let current_nav_link = "";

	let show_nav = false;
	import DropDown from "$lib/components/VersionDropdown.svelte";
</script>

<section
	class="top-0 left-0 fixed flex items-center p-4 rounded-br-lg backdrop-blur-lg z-50 bg-gray-200/50 lg:hidden"
	id="menu-bar"
>
	<button
		on:click={() => (show_nav = !show_nav)}
		type="button"
		class="text-slate-500 hover:text-slate-600 dark:text-slate-400 dark:hover:text-slate-300"
	>
		<svg width="24" height="24"
			><path
				d="M5 6h14M5 12h14M5 18h14"
				fill="none"
				stroke="currentColor"
				stroke-width="2"
				stroke-linecap="round"
			/></svg
		>
	</button>
</section>

<div
	use:clickOutside
	on:click_outside={() => (show_nav = false)}
	class:hidden={!show_nav}
	class="max-w-max md:min-w-[200px] navigation mobile-nav overflow-y-auto fixed backdrop-blur-lg z-50 bg-gray-200/50 pr-6 pl-4 py-4 -ml-4 h-full inset-0 lg:inset-auto lg:ml-0 lg:z-0 lg:backdrop-blur-none lg:navigation lg:p-0 lg:pb-4 lg:h-screen lg:leading-relaxed lg:sticky lg:top-0 lg:text-md lg:block rounded-t-xl lg:bg-gradient-to-r lg:from-white lg:to-gray-50 lg:overflow-x-clip lg:w-2/12"
	id="mobile-nav"
>
	<button
		on:click={() => (show_nav = !show_nav)}
		type="button"
		class="absolute z-10 top-4 right-4 w-2/12 h-4 flex items-center justify-center text-grey-500 hover:text-slate-600 dark:text-slate-400 dark:hover:text-slate-300 p-4 lg:hidden"
		tabindex="0"
	>
		<svg viewBox="0 0 10 10" class="overflow-visible" style="width: 10px"
			><path
				d="M0 0L10 10M10 0L0 10"
				fill="none"
				stroke="currentColor"
				stroke-width="2"
				stroke-linecap="round"
			/></svg
		>
	</button>

	<div
		class="w-full sticky top-0 bg-gradient-to-r from-white to-gray-50 z-10 hidden lg:block my-4 ml-4"
	>
		<DropDown></DropDown>
	</div>

	{#each library_pages as category_pages}
		<p class="font-semibold px-4 my-2 block">{category_pages.category}</p>
		{#each category_pages.pages as page}
			<a
				class:current-nav-link={current_nav_link == page.name}
				class="thin-link px-4 block leading-8"
				href={page.name}>{page.pretty_name}</a
			>
		{/each}
	{/each}
</div>
