<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	let is_mobile = false;
	let menu_open = false;
	let nav_visible = true;
	let prev_scrollY: number;
	function toggleMenu() {
		menu_open = !menu_open;
		document.body.style.overflow = menu_open ? 'hidden' : 'auto';
	}

	function handleOverlayClick() {
		toggleMenu()
	}
	function checkMobile() {
		is_mobile = window.matchMedia('(max-width: 768px)').matches;
	}
	function checkNavShouldBeVisible() {
		if (window.scrollY > 200 && window.scrollY > prev_scrollY) {
			nav_visible = false
		}
		else if (window.scrollY < prev_scrollY) {

      	nav_visible = true;
    }
    prev_scrollY = window.scrollY;
  }


	onMount(() => {
		checkMobile();
		window.addEventListener('resize', checkMobile);
		window.addEventListener('scroll', checkNavShouldBeVisible)
	});
</script>

<nav>
	{#if is_mobile && nav_visible}
		<div class="navbar-mobile" role="navigation" transition:slide={{ delay: 250, duration: 300, easing: quintOut, axis: 'y' }}>
			<button on:click={toggleMenu} aria-expanded={menu_open} aria-controls="mobile-menu">
				Hamburger
			</button>
		</div>
	{:else if !is_mobile && nav_visible}
		<div role="navigation" aria-label="Main Navigation" class="navbar-desktop" transition:slide={{ delay: 250, duration: 300, easing: quintOut, axis: 'y' }}>
			<a href="/">Home</a>
			<a href="/about">About</a>
			<a href="/settings">Plans & Pricing</a>
		</div>
	{/if}
	<p>{`isMobile: ${is_mobile}`}</p>
	{#if menu_open}
		<div
			class="overlay"
			on:click={handleOverlayClick}
			role="presentation"
			transition:fade={{ delay: 250, duration: 300, easing: quintOut }}
		></div>
		<div
			class="main-nav-mobile"
			role="navigation"
			aria-label="Main Navigation"
			aria-hidden={!menu_open}
			transition:slide={{ delay: 250, duration: 300, easing: quintOut, axis: 'x' }}
		>
			<a href="#home">Home</a>
			<a href="#about">About</a>
			<a href="#services">Plans & Pricing</a>
		</div>
	{/if}
</nav>

<slot></slot>

<style>
	.main-nav-mobile {
		position: fixed;
		top: 0;
		left: 0;
		height: 100%;
		width: 250px;
		background: #333;
		color: white;
		overflow-y: auto;
		white-space: nowrap;
	}

	.main-nav-mobile a {
		display: block;
		padding: 1em;
		color: white;
		text-decoration: none;
	}

	.main-nav-mobile a:hover {
		background: #444;
	}
	.navbar-mobile {
		background-color: #458dc0;
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 5rem;
	}

	.navbar-desktop {
		background-color: #458dc0;
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 5rem;
	}

	.overlay {
		display: block;
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
	}
</style>
