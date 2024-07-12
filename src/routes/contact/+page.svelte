<script lang="ts">
	import Textfield from '@smui/textfield';
	import CharacterCounter from '@smui/textfield/character-counter';
	import Snackbar, { Label, Actions } from '@smui/snackbar';
	import LinearProgress from '@smui/linear-progress';
	import IconButton from '@smui/icon-button';
	import Button from '@smui/button';
	import { onDestroy } from 'svelte';
	let valueA = '';
	let valueB = '';
	let valueC = '';
	let progress = 0;
	let closed = true;
	let timer: number;
	let snackbarSuccess: Snackbar;
	function handleSubmit() {
		progress = 0;
		reset();
	}
	onDestroy(() => {
		clearInterval(timer);
	});

	function reset() {
		progress = 0;
		closed = false;
		clearInterval(timer);
		timer = setInterval(() => {
			progress += 0.1;

			if (progress >= 1) {
				progress = 1;
				closed = true;
				clearInterval(timer);
				snackbarSuccess.open();
				valueA = '';
				valueB = '';
				valueC = '';
			}
		}, 100);
	}
</script>

<main>
	<section class="head-section">
		<div class="banner-outer">
			<div class="banner-inner">
				<h2>Contact</h2>
				<svg
					style="margin-top: 2rem;"
					class="banner-icon"
					width="120"
					height="125"
					viewBox="0 0 91 75"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						d="M6 0C5.07012 0 4.19031 0.21931 3.40625 0.59375L37.1875 34.75C38.7578 36.3398 41.1768 36.3399 42.75 34.75L76.5938 0.59375C75.8097 0.21931 74.9299 0 74 0H6ZM79.4062 3.40625L54.0312 29.0625L79.4062 52.625C79.7883 51.8346 80 50.9399 80 50V6C80 5.07012 79.7807 4.19031 79.4062 3.40625ZM0.5625 3.43744C0.19914 4.21209 0 5.08484 0 6V50C0 50.9399 0.2117 51.8346 0.59375 52.625L25.9375 29.0938L0.5625 3.43744ZM51.1875 31.9062L45.5938 37.5625C42.5046 40.6842 37.4316 40.6885 34.3438 37.5625L28.7812 31.9375L3.46875 55.4374C4.23685 55.7934 5.09484 56 6 56H74C74.9052 56 75.7631 55.7934 76.5312 55.4375L51.1875 31.9062Z"
						fill="currentColor"
					/>
				</svg>
			</div>
		</div>
		<div class="form-container">
			<div class="contact-information-container">
				<div>
					<h3>Address</h3>
					<p>1234 Main St, Anytown, USA</p>
				</div>
				<div>
					<h3>Phone</h3>
					<p>(123) 456-7890</p>
				</div>
				<div>
					<h3>Email</h3>
					<p>godotgurus@gmail.com</p>
				</div>
				<h3>Follow Us!</h3>
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
			</div>
			<form on:submit={handleSubmit}>
				<div>
					<Textfield bind:value={valueA} label="Your Name" required style="width: 20rem;" />
				</div>
				<div>
					<Textfield
						bind:value={valueB}
						label="Your Email"
						required
						type="email"
						style="width: 20rem;"
					/>
				</div>
				<div>
					<Textfield
						textarea
						input$maxlength={100}
						bind:value={valueC}
						required
						label="Your Message"
						style="width: 20rem; height: 15rem;"
					>
						<CharacterCounter slot="internalCounter">0 / 100</CharacterCounter>
					</Textfield>
				</div>
				<Button type="submit" touch variant="raised" style="width: 20rem;">send message</Button>
				<LinearProgress {progress} {closed} />
			</form>
		</div>
	</section>
	<Snackbar bind:this={snackbarSuccess}>
		<Label>Message Sent! We'll get back to you ASAP &lt;3</Label>
		<Actions>
			<IconButton class="material-icons" title="Dismiss">close</IconButton>
		</Actions>
	</Snackbar>
</main>

<style>
	h2 {
		font-size: 4rem;
		max-width: max-content;
	}
	h3 {
		font-size: 1.5rem;
		line-height: 1.5rem;
		font-weight: 400;
	}
	p {
		line-height: 1.5rem;
		font-size: 1.2rem;
	}
	main {
		padding-top: 4rem;
		font-family: 'Montserrat', sans-serif;
		background-color: var(--bg-color-page);
		color: var(--text-color);
		width: 100%;
	}
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.banner-outer {
		width: 100%;
		background-color: var(--bg-color-banner);
		overflow-x: hidden;
	}
	.banner-inner {
		padding-left: 1rem;
		padding-right: 1rem;
		display: flex;
		gap: 2rem;
		align-items: center;
		justify-content: flex-start;
		margin-left: auto;
		margin-right: auto;
		max-width: fit-content;
	}
	.banner-icon {
		flex-shrink: 0;
		display: block;
	}
	@media (max-width: 1000px) {
		.contact-information-container {
			display: none !important;
		}
	}
	.head-section {
		margin-left: auto;
		margin-right: auto;
	}
	form {
		display: flex;
		flex-direction: column;
		gap: 2rem;
		padding-bottom: 2rem;
		padding-top: 2rem;
	}
	.form-container {
		display: flex;
		flex-direction: row-reverse;
		gap: 8rem;
	}
	.social-media {
		width: 100%;
		display: flex;
		gap: 2rem;
	}
	.contact-information-container {
		display: flex;
		flex-direction: column;
		justify-content: start;
		text-align: left;
		gap: 0.5rem;
		margin-top: 2rem;
	}
</style>
