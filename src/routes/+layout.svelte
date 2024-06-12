<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import Button from '@smui/button';
	import '../app.css'
	let is_mobile = false;
	let menu_open = false;
	let nav_visible = true;
	let prev_scrollY: number;

	function setThemeOnLoad() {
    const storedTheme = sessionStorage.getItem('theme');
    const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)").matches;

    if (storedTheme === 'dark' || (storedTheme === null && prefersDarkScheme)) {
      document.documentElement.classList.add('dark-mode');
	  sessionStorage.setItem('theme', 'dark')
	  removeStylesheet('smui.css');
      addStylesheet('smui-dark.css');
    } else {
      document.documentElement.classList.remove('dark-mode');
	  sessionStorage.setItem('theme', 'light')
	  removeStylesheet('smui-dark.css');
      addStylesheet('smui.css');
    }
  }
  function toggleTheme() {
	let theme = sessionStorage.getItem('theme')
		if (theme === 'dark') {
			sessionStorage.setItem('theme', 'light')
			document.documentElement.classList.remove('dark-mode');
			removeStylesheet('smui-dark.css');
      		addStylesheet('smui.css');
		}
		else if (theme === 'light') {
			sessionStorage.setItem('theme', 'dark')
			document.documentElement.classList.add('dark-mode');
			removeStylesheet('smui.css');
      		addStylesheet('smui-dark.css');
		}
  }
	function toggleMenu() {
		menu_open = !menu_open;
		document.body.style.overflow = menu_open ? 'hidden' : 'auto';
	}

	function handleOverlayClick() {
		toggleMenu();
	}
	function checkMobile() {
		is_mobile = window.matchMedia('(max-width: 768px)').matches;
	}
	function checkNavShouldBeVisible() {
		if (window.scrollY > 200 && window.scrollY > prev_scrollY) {
			nav_visible = false;
		} else if (window.scrollY < prev_scrollY) {
			nav_visible = true;
		}
		prev_scrollY = window.scrollY;
	}
	function addStylesheet(name:String) {
    const link = document.createElement('link');
    link.rel = 'stylesheet';
    link.href = `/${name}`;
    document.head.appendChild(link);
  }

  function removeStylesheet(name:String) {
    const links = document.head.querySelectorAll(`link[href="/${name}"]`);
    links.forEach(link => link.remove());
  }

	onMount(() => {
		setThemeOnLoad();
		checkMobile();
		window.addEventListener('resize', checkMobile);
		window.addEventListener('scroll', checkNavShouldBeVisible);
	});
</script>

<main>
	<nav>
		{#if is_mobile && nav_visible}
			<div
				class="navbar-mobile"
				role="navigation"
				transition:slide={{ delay: 100, duration: 300, easing: quintOut, axis: 'y' }}
			>
				<a href="/" class="logo-container">
					<img class="logo-image" src="logo-godot-guru.png" alt="logo" />
					<strong style="color: white;">GODOT GURU</strong>
				</a>
				<button
					class={`hamburger hamburger--collapse ${menu_open ? 'is-active' : ''}`}
					on:click={toggleMenu}
					aria-expanded={menu_open}
					aria-controls="mobile-menu"
				>
					<span class="hamburger-box">
						<span class="hamburger-inner"></span>
					</span>
				</button>
			</div>
		{:else if !is_mobile && nav_visible}
			<div
				role="navigation"
				aria-label="Main Navigation"
				class="navbar-desktop"
				transition:slide={{ delay: 100, duration: 300, easing: quintOut, axis: 'y' }}
			>
				<a href="/" class="logo-container">
					<img class="logo-image" src="logo-godot-guru.png" alt="logo" />
					<strong>GODOT GURU</strong>
				</a>

				<div>
					<a href="/about">About</a>
					<a href="/contact">Contact</a>
					<a href="/settings">Plans & Pricing</a>
					<Button on:click={toggleTheme}>TOGGLE DARK MODE</Button>
				</div>
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
				<a href="#about">About</a>
				<a href="/contact">Contact</a>
				<a href="#services">Plans & Pricing</a>
			</div>
		{/if}
	</nav>
	<slot></slot>
	<footer>
		<p>&copy; 2024 Godot Guru. All rights reserved.</p>
		<nav class="footer-nav">
			<a href="/">Home</a>
			<a href="/about">About</a>
			<a href="/contact">Contact</a>
			<a href="/privacy-policy">Plans & Pricing</a>
		</nav>
		<div class="social-media">
			<a
				href="https://www.facebook.com"
				aria-label="Facebook"
				target="_blank"
				rel="noopener noreferrer"
			>
				<img src="facebook-icon.png" alt="Facebook" />
			</a>
			<a
				href="https://www.twitter.com"
				aria-label="Twitter"
				target="_blank"
				rel="noopener noreferrer"
			>
				<img src="twitter-icon.png" alt="Twitter" />
			</a>
			<a
				href="https://www.instagram.com"
				aria-label="Instagram"
				target="_blank"
				rel="noopener noreferrer"
			>
				<img src="instagram-icon.png" alt="Instagram" />
			</a>
		</div>
	</footer>
</main>

<style>
	@import 'hamburgers/dist/hamburgers.css';
	:global(body) {
		margin: 0px;
	}
	.logo-image {
		filter: var(--filter-invert);
		height: 4rem;
		width: 4rem;
	}
	.logo-container {
		color: var(--text-color);
		text-decoration: none;
		display: flex;
		align-items: center;
		gap: 1rem;
		cursor: pointer;
	}
	.main-nav-mobile {
		margin-top: 5rem;
		font-family: 'Montserrat', sans-serif;
		position: fixed;
		top: 0;
		right: 0;
		height: 100%;
		width: 250px;
		background: var(--bg-color-page);
		color: white;
		overflow-y: auto;
		white-space: nowrap;
		z-index: 2;
	}

	.main-nav-mobile a {
		display: block;
		padding: 1em;
		color: white;
		text-decoration: none;
	}
	.navbar-mobile {
		font-family: 'Montserrat', sans-serif;
		background-color: var(--bg-color-nav);
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 5rem;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 1rem;
		box-sizing: border-box;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Box shadow */
		z-index: 3;
	}

	.navbar-desktop {
		font-family: 'Montserrat', sans-serif;
		background-color: var(--bg-color-nav);
		position: fixed;
		top: 0;
		left: 0;
		height: 5rem;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 2rem;
		box-sizing: border-box;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
		z-index: 1;
	}
	.navbar-desktop a {
		color: var(--text-color);
		padding: 1rem;
	}

	.overlay {
		display: block;
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		z-index: 1;
	}
	footer {
		position: relative;
		padding: 2rem;
		font-family: 'Montserrat', sans-serif;
		height: 15rem;
		background-color: var(--bg-color-nav);
		color: var(--text-color);
		display: flex;
		align-items: center;
		justify-content: space-evenly;
		gap: 1rem;
		z-index: 1;
	}
	footer a {
		color: var(--text-color);
	}
	.footer-nav {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}
	.social-media {
		display: flex;
		flex-wrap: wrap;
		gap: 2rem;
	}
</style>
