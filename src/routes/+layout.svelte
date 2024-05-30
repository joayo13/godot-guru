<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	let isMobile = false;
	let menuOpen = false;

	function toggleMenu() {
		menuOpen = !menuOpen;
		if (menuOpen === true) {
			document.addEventListener('keydown', handleKeydown);
		}
		else {
			document.removeEventListener('keydown', handleKeydown);
		}
	}

	function handleKeydown(event: KeyboardEvent) {
		if (event.key === 'Escape' && menuOpen) {
			menuOpen = false;
		}
	}

	function handleOverlayClick() {
		menuOpen = false;
	}
	function checkMobile() {
		isMobile = window.matchMedia('(max-width: 768px)').matches;
	}

	onMount(() => {
		checkMobile();
		window.addEventListener('resize', checkMobile);
	});
</script>

<nav>
	{#if isMobile}
		<button on:click={toggleMenu} aria-expanded={menuOpen} aria-controls="mobile-menu">
			Hamburger
		</button>
	{:else}
		<div role="navigation" aria-label="Main Navigation" class="main-nav">
			<a href="/">Home</a>
			<a href="/about">About</a>
			<a href="/settings">Settings</a>
		</div>
	{/if}
	<p>{`isMobile: ${isMobile}`}</p>
	{#if menuOpen}
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
			aria-hidden={!menuOpen}
			transition:slide={{ delay: 250, duration: 300, easing: quintOut, axis: 'x' }}
		>
			<a href="#home">Home</a>
			<a href="#about">About</a>
			<a href="#services">Services</a>
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
