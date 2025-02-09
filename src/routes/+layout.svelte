<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import '../app.css';
	import { onNavigate } from '$app/navigation';
	let is_mobile = false;
	let menu_open = false;
	let nav_visible = true;
	let prev_scrollY: number;
	let isThemeSwitchDark = false;
	

	onNavigate((navigation) => {
		if (!document.startViewTransition) return;

		return new Promise((resolve) => {
			document.startViewTransition(async () => {
				resolve();
				await navigation.complete;
			});
		});
	});

	function setThemeOnLoad() {
		const storedTheme = sessionStorage.getItem('theme');
		const prefersDarkScheme = window.matchMedia('(prefers-color-scheme: dark)').matches;

		if (storedTheme === 'dark' || (storedTheme === null && prefersDarkScheme)) {
			document.documentElement.classList.add('dark-mode');
			sessionStorage.setItem('theme', 'dark');
			addStylesheet('smui-dark.css');
			removeStylesheet('smui.css');
			isThemeSwitchDark = true;
		} else {
			document.documentElement.classList.remove('dark-mode');
			sessionStorage.setItem('theme', 'light');
			addStylesheet('smui.css');
			removeStylesheet('smui-dark.css');
		}
	}
	function toggleTheme() {
		let theme = sessionStorage.getItem('theme');
		if (theme === 'dark') {
			sessionStorage.setItem('theme', 'light');
			addStylesheet('smui.css');
			removeStylesheet('smui-dark.css');
			document.documentElement.classList.remove('dark-mode');
			isThemeSwitchDark = false;
		} else if (theme === 'light') {
			sessionStorage.setItem('theme', 'dark');
			addStylesheet('smui-dark.css');
			removeStylesheet('smui.css');
			document.documentElement.classList.add('dark-mode');
			isThemeSwitchDark = true;
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
	function addStylesheet(name: String) {
		const link = document.createElement('link');
		link.rel = 'stylesheet';
		link.href = `/${name}`;
		document.head.appendChild(link);
	}

	function removeStylesheet(name: String) {
		const links = document.head.querySelectorAll(`link[href="/${name}"]`);
		links.forEach((link) => link.remove());
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
				<div style="flex-grow: 1;"></div>
				<div class="navbar-links">
					<a href="/about">About</a>
					<a href="/contact">Contact</a>
					<a href="/plans">Plans & Pricing</a>
				</div>
				<button
					aria-label={isThemeSwitchDark ? 'Switch to light mode' : 'Switch to dark mode'}
					aria-pressed={isThemeSwitchDark}
					class="theme-switch-container"
					on:click={toggleTheme}
				>
					<span class={`theme-switch-knob ${isThemeSwitchDark ? 'theme-switch-dark' : ''} `}>
						{#if isThemeSwitchDark}
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class="size-6"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M21.752 15.002A9.72 9.72 0 0 1 18 15.75c-5.385 0-9.75-4.365-9.75-9.75 0-1.33.266-2.597.748-3.752A9.753 9.753 0 0 0 3 11.25C3 16.635 7.365 21 12.75 21a9.753 9.753 0 0 0 9.002-5.998Z"
								/>
							</svg>
						{:else}
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class="size-6"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M12 3v2.25m6.364.386-1.591 1.591M21 12h-2.25m-.386 6.364-1.591-1.591M12 18.75V21m-4.773-4.227-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Z"
								/>
							</svg>
						{/if}
					</span>
				</button>
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
				<a on:click={toggleMenu} href="/about">About</a>
				<a on:click={toggleMenu} href="/contact">Contact</a>
				<a on:click={toggleMenu} href="/plans">Plans & Pricing</a>
				<div class="main-nav-mobile-divider"></div>
				<button
					aria-label={isThemeSwitchDark ? 'Switch to light mode' : 'Switch to dark mode'}
					aria-pressed={isThemeSwitchDark}
					class="theme-switch-container-mobile"
					on:click={toggleTheme}
				>
					<span class={`theme-switch-knob ${isThemeSwitchDark ? 'theme-switch-dark' : ''} `}>
						{#if isThemeSwitchDark}
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class="size-6"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M21.752 15.002A9.72 9.72 0 0 1 18 15.75c-5.385 0-9.75-4.365-9.75-9.75 0-1.33.266-2.597.748-3.752A9.753 9.753 0 0 0 3 11.25C3 16.635 7.365 21 12.75 21a9.753 9.753 0 0 0 9.002-5.998Z"
								/>
							</svg>
						{:else}
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class="size-6"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M12 3v2.25m6.364.386-1.591 1.591M21 12h-2.25m-.386 6.364-1.591-1.591M12 18.75V21m-4.773-4.227-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Z"
								/>
							</svg>
						{/if}
					</span>
				</button>
			</div>
		{/if}
	</nav>
	<slot></slot>
	<footer>
		<p>
			Created with ☕ by <a
				href="https://www.github.com/joayo13"
				aria-label="Github Profile"
				target="_blank"
				rel="noopener noreferrer">joayo13</a
			>
		</p>
		<nav class="footer-nav">
			<a href="/">Home</a>
			<a href="/about">About</a>
			<a href="/contact">Contact</a>
			<a href="/plans">Plans & Pricing</a>
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
	:global(body) {
		margin: 0px;
	}
	
	button {
		-webkit-tap-highlight-color: transparent;
		-webkit-tap-highlight-color: rgba(0, 0, 0, 0);
	}
	.theme-switch-container {
		display: block;
		position: relative;
		width: 3rem;
		height: 1.5rem;
		border-radius: 1rem;
		border: 1px solid var(--text-color);
		background-color: transparent;
		opacity: 0.6;
		cursor: pointer;
	}
	.theme-switch-container-mobile {
		display: block;
		position: relative;
		width: 3rem;
		height: 1.5rem;
		border-radius: 1rem;
		border: 1px solid var(--text-color);
		background-color: transparent;
		opacity: 0.6;
		cursor: pointer;
	}
	.theme-switch-container:focus {
		opacity: 1;
	}
	.theme-switch-container:hover {
		opacity: 1;
	}
	.theme-switch-knob {
		position: absolute;
		top: 1px;
		left: 1px;
		width: 1.25rem;
		height: 1.25rem;
		border-radius: 50%;
		background-color: var(--bg-color-page);
		color: var(--text-color);
	}
	.theme-switch-dark {
		transform: translateX(23px);
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
		padding: 1rem;
		margin-top: 5rem;
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
		position: fixed;
		top: 0;
		right: 0;
		height: 100%;
		width: 250px;
		background: var(--bg-color-page);
		color: var(--text-color);
		overflow-y: auto;
		white-space: nowrap;
		z-index: 2;
	}
	.main-nav-mobile-divider {
		height: 1px;
		background-color: var(--text-color);
		width: 100%;
		margin-top: 1rem;
		margin-bottom: 2rem;
	}

	.main-nav-mobile a {
		display: block;
		color: var(--text-color);
		text-decoration: underline;
		padding-top: 1rem;
		padding-bottom: 1rem;
	}
	.navbar-mobile {
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
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
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
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
	@media screen and (max-width: 1100px) {
		.navbar-links {
			display: none !important;
		}
		.hamburger {
			display: inline-block !important;
		}
		.theme-switch-container {
			display: none;
		}
	}
	.navbar-links {
		display: block;
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
		z-index: 2;
	}
	footer {
		position: relative;
		padding: 2rem;
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
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
		justify-content: center;
		gap: 2rem;
	}
	/*!
 * Hamburgers
 * @description Tasty CSS-animated hamburgers
 * @author Jonathan Suh @jonsuh
 * @site https://jonsuh.com/hamburgers
 * @link https://github.com/jonsuh/hamburgers
 */
	.hamburger {
		padding: 15px 15px;
		display: none;
		cursor: pointer;
		transition-property: opacity, filter;
		transition-duration: 0.15s;
		transition-timing-function: linear;
		font: inherit;
		color: inherit;
		text-transform: none;
		background-color: transparent;
		border: 0;
		margin: 0;
		overflow: visible;
	}
	.hamburger.is-active .hamburger-inner,
	.hamburger.is-active .hamburger-inner::before,
	.hamburger.is-active .hamburger-inner::after {
		background-color: var(--text-color);
	}

	.hamburger-box {
		width: 40px;
		height: 24px;
		display: inline-block;
		position: relative;
	}

	.hamburger-inner {
		display: block;
		top: 50%;
		margin-top: -2px;
	}
	.hamburger-inner,
	.hamburger-inner::before,
	.hamburger-inner::after {
		width: 40px;
		height: 4px;
		background-color: var(--text-color);
		border-radius: 4px;
		position: absolute;
		transition-property: transform;
		transition-duration: 0.15s;
		transition-timing-function: ease;
	}
	.hamburger-inner::before,
	.hamburger-inner::after {
		content: '';
		display: block;
	}
	.hamburger-inner::before {
		top: -10px;
	}
	.hamburger-inner::after {
		bottom: -10px;
	}

	/*
     * Collapse
     */
	.hamburger--collapse .hamburger-inner {
		top: auto;
		bottom: 0;
		transition-duration: 0.13s;
		transition-delay: 0.13s;
		transition-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
	}
	.hamburger--collapse .hamburger-inner::after {
		top: -20px;
		transition:
			top 0.2s 0.2s cubic-bezier(0.33333, 0.66667, 0.66667, 1),
			opacity 0.1s linear;
	}
	.hamburger--collapse .hamburger-inner::before {
		transition:
			top 0.12s 0.2s cubic-bezier(0.33333, 0.66667, 0.66667, 1),
			transform 0.13s cubic-bezier(0.55, 0.055, 0.675, 0.19);
	}

	.hamburger--collapse.is-active .hamburger-inner {
		transform: translate3d(0, -10px, 0) rotate(-45deg);
		transition-delay: 0.22s;
		transition-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
	}
	.hamburger--collapse.is-active .hamburger-inner::after {
		top: 0;
		opacity: 0;
		transition:
			top 0.2s cubic-bezier(0.33333, 0, 0.66667, 0.33333),
			opacity 0.1s 0.22s linear;
	}
	.hamburger--collapse.is-active .hamburger-inner::before {
		top: 0;
		transform: rotate(-90deg);
		transition:
			top 0.1s 0.16s cubic-bezier(0.33333, 0, 0.66667, 0.33333),
			transform 0.13s 0.25s cubic-bezier(0.215, 0.61, 0.355, 1);
	}

	/*
     * Collapse Reverse
     */
	.hamburger--collapse-r .hamburger-inner {
		top: auto;
		bottom: 0;
		transition-duration: 0.13s;
		transition-delay: 0.13s;
		transition-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
	}
	.hamburger--collapse-r .hamburger-inner::after {
		top: -20px;
		transition:
			top 0.2s 0.2s cubic-bezier(0.33333, 0.66667, 0.66667, 1),
			opacity 0.1s linear;
	}
	.hamburger--collapse-r .hamburger-inner::before {
		transition:
			top 0.12s 0.2s cubic-bezier(0.33333, 0.66667, 0.66667, 1),
			transform 0.13s cubic-bezier(0.55, 0.055, 0.675, 0.19);
	}

	.hamburger--collapse-r.is-active .hamburger-inner {
		transform: translate3d(0, -10px, 0) rotate(45deg);
		transition-delay: 0.22s;
		transition-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
	}
	.hamburger--collapse-r.is-active .hamburger-inner::after {
		top: 0;
		opacity: 0;
		transition:
			top 0.2s cubic-bezier(0.33333, 0, 0.66667, 0.33333),
			opacity 0.1s 0.22s linear;
	}
	.hamburger--collapse-r.is-active .hamburger-inner::before {
		top: 0;
		transform: rotate(90deg);
		transition:
			top 0.1s 0.16s cubic-bezier(0.33333, 0, 0.66667, 0.33333),
			transform 0.13s 0.25s cubic-bezier(0.215, 0.61, 0.355, 1);
	}
</style>
