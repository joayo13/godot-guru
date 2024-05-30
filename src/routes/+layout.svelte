<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	let isMobile = false;
	let menuOpen = false;

	function toggleMenu() {
		menuOpen = !menuOpen;
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
		//Listen for escape key when if mobile menu is open
		if (typeof document !== 'undefined') {
			if (menuOpen) {
				document.body.style.overflow = 'hidden';
				document.addEventListener('keydown', handleKeydown);
			} else {
				document.body.style.overflow = 'auto';
				document.removeEventListener('keydown', handleKeydown);
			}
		}

		return () => {
			window.removeEventListener('resize', checkMobile);
		};
	});
</script>

<nav class="navbar">
	{#if isMobile}
		<button on:click={toggleMenu}>Hamburger</button>
	{:else}
		<a href="/">Home</a>
		<a href="/about">About</a>
		<a href="/settings">Settings</a>
	{/if}
	<p>{`isMobile: ${isMobile}`}</p>
	{#if menuOpen}
		<div
			class="overlay"
			on:click={handleOverlayClick}
			role="presentation"
			transition:fade={{ delay: 250, duration: 300, easing: quintOut }}
		></div>
		<nav
			class="mobile-menu"
			aria-hidden={!menuOpen}
			transition:slide={{ delay: 250, duration: 300, easing: quintOut, axis: 'x' }}
		>
			<a href="#home">Home</a>
			<a href="#about">About</a>
			<a href="#services">Services</a>
		</nav>
	{/if}
</nav>

<slot></slot>

<style>
	.mobile-menu {
		position: fixed;
		top: 0;
		left: 0;
		height: 100%;
		width: 250px;
		background: #333;
		color: white;
		overflow-y: auto;
	}

	.mobile-menu a {
		display: block;
		padding: 1em;
		color: white;
		text-decoration: none;
	}

	.mobile-menu a:hover {
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
