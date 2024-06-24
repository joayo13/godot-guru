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
		<div class="banner">
			<h2 style="margin-left: 1rem;">Contact Form</h2>
			<svg
				style="margin-top: 1rem;"
				class="banner-icon"
				width="182"
				height="150"
				viewBox="0 0 91 75"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
			>
				<path
					fill-rule="evenodd"
					clip-rule="evenodd"
					d="M52.49 69.11H27.94C27.2 69.11 26.53 69.41 26.04 69.9C25.55 70.39 25.25 71.06 25.25 71.8V74.49H55.18V71.8C55.18 71.06 54.88 70.39 54.39 69.9C53.9 69.41 53.23 69.11 52.49 69.11ZM47.83 61.41H32.61L32.02 66.9H48.42L47.83 61.41ZM18.86 22.48L15.52 24.41C12.67 26.06 12.66 30.38 14.19 35.01C14.82 36.92 15.7 38.86 16.76 40.7C16.77 40.72 16.78 40.74 16.79 40.76C17.87 42.63 19.12 44.39 20.46 45.89C23.71 49.53 27.46 51.68 30.31 50.04L33.58 48.15C33.58 48.15 33.65 48.1 33.69 48.08C33.86 47.97 33.98 47.8 34.03 47.61C34.08 47.42 34.07 47.21 33.97 47.03C33.94 46.99 33.92 46.94 33.89 46.89L31.52 42.78C31.52 42.78 31.5 42.74 31.48 42.72C31.37 42.52 31.18 42.39 30.98 42.34C30.77 42.28 30.55 42.31 30.36 42.42L28.05 43.76C27.32 44.18 26.5 44.26 25.75 44.06C25 43.86 24.33 43.37 23.91 42.65L18.75 33.72C18.74 33.7 18.73 33.68 18.71 33.66C18.29 32.93 18.21 32.11 18.41 31.36C18.61 30.61 19.1 29.94 19.82 29.52L22.08 28.22C22.1 28.21 22.12 28.2 22.14 28.18C22.34 28.07 22.47 27.88 22.52 27.68C22.58 27.47 22.55 27.25 22.44 27.06L19.98 22.8C19.87 22.6 19.68 22.47 19.48 22.42C19.27 22.36 19.05 22.39 18.86 22.5V22.48ZM14.41 22.5L17.75 20.57C18.48 20.15 19.3 20.07 20.05 20.27C20.8 20.47 21.47 20.96 21.89 21.68L24.35 25.94C24.77 26.67 24.85 27.49 24.65 28.24C24.45 28.99 23.96 29.66 23.24 30.08C23.22 30.09 23.2 30.1 23.18 30.11L20.93 31.41C20.73 31.52 20.6 31.71 20.55 31.91C20.49 32.12 20.52 32.34 20.63 32.53C20.64 32.55 20.65 32.57 20.66 32.59L25.81 41.52C25.92 41.71 26.11 41.85 26.31 41.9C26.52 41.96 26.74 41.93 26.93 41.82L29.24 40.48C29.97 40.06 30.79 39.98 31.54 40.18C32.29 40.38 32.96 40.87 33.38 41.59C33.39 41.61 33.4 41.63 33.41 41.65L35.84 45.85C36.26 46.57 36.34 47.4 36.14 48.15C35.94 48.9 35.45 49.57 34.73 49.99L31.39 51.92C27.44 54.2 22.71 51.73 18.79 47.33C17.34 45.71 16 43.82 14.85 41.84C14.84 41.82 14.83 41.8 14.82 41.78C13.68 39.8 12.73 37.71 12.06 35.68C10.22 30.08 10.44 24.75 14.39 22.47L14.41 22.5ZM29.19 25.68C28.6 25.52 28.25 24.92 28.41 24.33C28.57 23.74 29.17 23.39 29.76 23.55C32.93 24.4 35.47 26.46 36.99 29.1C38.52 31.74 39.03 34.96 38.18 38.14C38.02 38.73 37.42 39.08 36.83 38.92C36.24 38.76 35.89 38.16 36.05 37.57C36.74 34.98 36.32 32.35 35.08 30.21C33.84 28.06 31.78 26.39 29.19 25.69V25.68ZM28.28 29.06C27.69 28.9 27.34 28.3 27.5 27.71C27.66 27.12 28.26 26.77 28.85 26.93C31.09 27.53 32.88 28.99 33.96 30.85C35.04 32.72 35.4 34.99 34.8 37.24C34.64 37.83 34.04 38.18 33.45 38.02C32.86 37.86 32.51 37.26 32.67 36.67C33.11 35.01 32.85 33.33 32.05 31.96C31.26 30.59 29.94 29.52 28.28 29.07V29.06ZM27.37 32.44C26.78 32.28 26.43 31.68 26.59 31.09C26.75 30.5 27.35 30.15 27.94 30.31C29.25 30.66 30.3 31.51 30.93 32.6C31.56 33.69 31.77 35.02 31.42 36.33C31.26 36.92 30.66 37.27 30.07 37.11C29.48 36.95 29.13 36.35 29.29 35.76C29.48 35.04 29.37 34.3 29.02 33.7C28.67 33.1 28.1 32.63 27.37 32.44ZM58.4 22.38L45.67 15.03L48.36 25.07L58.4 22.38ZM45.43 12.34C44.9 12.03 44.29 11.97 43.75 12.12C43.23 12.26 42.76 12.59 42.45 13.07C42.43 13.1 42.41 13.12 42.4 13.15L36.72 22.99C36.41 23.52 36.35 24.13 36.5 24.67C36.64 25.19 36.97 25.66 37.45 25.97C37.48 25.99 37.5 26.01 37.53 26.02L52.94 34.92C53.47 35.23 54.08 35.29 54.62 35.14C55.14 35 55.61 34.67 55.92 34.19C55.94 34.16 55.96 34.14 55.97 34.11L61.65 24.27C61.96 23.74 62.02 23.13 61.87 22.59C61.73 22.07 61.4 21.6 60.92 21.29C60.89 21.27 60.87 21.25 60.84 21.24L45.43 12.34ZM39.4 22.76L43.53 15.6L45.04 21.24L39.4 22.75V22.76ZM53.33 26.03L58.97 24.52L54.84 31.68L53.33 26.04V26.03ZM52.71 32.25L39.98 24.9L45.62 23.39L46.51 26.72C46.67 27.31 47.27 27.66 47.86 27.5L51.19 26.61L52.7 32.25H52.71ZM68.2 24.29C68.03 24.41 67.86 24.52 67.71 24.62C67.21 24.97 67.09 25.66 67.44 26.16C67.68 26.5 68.06 26.66 68.45 26.62C70.32 26.5 72.5 25.97 74.55 25.1C75.01 24.91 75.46 24.69 75.9 24.46V55.17H4.54V8.75999H61.75C61.67 9.24999 61.63 9.74999 61.63 10.26C61.63 12.83 62.67 15.2 64.46 17.15C66.04 18.88 68.21 20.27 70.74 21.16C70.25 22.91 69.12 23.67 68.2 24.27V24.29ZM63.38 4.74999C62.99 5.32999 62.65 5.93999 62.38 6.57999H3.43C2.82 6.57999 2.32 7.07999 2.32 7.68999V56.29C2.32 56.9 2.82 57.4 3.43 57.4H76.99C77.6 57.4 78.1 56.9 78.1 56.29V23.09C78.5 22.79 78.89 22.47 79.24 22.14C79.47 22.12 79.7 22.09 79.93 22.06V58.92C79.93 59 79.9 59.08 79.84 59.13C79.79 59.18 79.71 59.22 79.63 59.22H0.8C0.72 59.22 0.64 59.19 0.59 59.13C0.54 59.08 0.5 59 0.5 58.92V5.01999C0.5 4.93999 0.53 4.85999 0.59 4.80999C0.64 4.75999 0.72 4.71999 0.8 4.71999H63.39L63.38 4.74999ZM70.14 9.61999C69.97 9.44999 69.73 9.33999 69.47 9.33999C69.21 9.33999 68.97 9.44999 68.8 9.61999C68.63 9.78999 68.52 10.03 68.52 10.29C68.52 10.55 68.63 10.79 68.8 10.96C68.97 11.13 69.21 11.24 69.47 11.24C69.73 11.24 69.97 11.13 70.14 10.96C70.31 10.79 70.42 10.55 70.42 10.29C70.42 10.03 70.31 9.78999 70.14 9.61999ZM69.47 7.12999C68.6 7.12999 67.81 7.47999 67.24 8.04999C66.67 8.61999 66.32 9.40999 66.32 10.28C66.32 11.15 66.67 11.94 67.24 12.51C67.81 13.08 68.6 13.43 69.47 13.43C70.34 13.43 71.13 13.08 71.7 12.51C72.27 11.94 72.62 11.15 72.62 10.28C72.62 9.40999 72.27 8.61999 71.7 8.04999C71.13 7.47999 70.34 7.12999 69.47 7.12999ZM77.83 9.61999C77.66 9.44999 77.42 9.33999 77.16 9.33999C76.9 9.33999 76.66 9.44999 76.49 9.61999C76.32 9.78999 76.21 10.03 76.21 10.29C76.21 10.55 76.32 10.79 76.49 10.96C76.66 11.13 76.9 11.24 77.16 11.24C77.42 11.24 77.66 11.13 77.83 10.96C78 10.79 78.11 10.55 78.11 10.29C78.11 10.03 78 9.78999 77.83 9.61999ZM77.16 7.12999C76.29 7.12999 75.5 7.47999 74.93 8.04999C74.36 8.61999 74.01 9.40999 74.01 10.28C74.01 11.15 74.36 11.94 74.93 12.51C75.5 13.08 76.29 13.43 77.16 13.43C78.03 13.43 78.82 13.08 79.39 12.51C79.96 11.94 80.31 11.15 80.31 10.28C80.31 9.40999 79.96 8.61999 79.39 8.04999C78.82 7.47999 78.03 7.12999 77.16 7.12999ZM85.52 9.61999C85.35 9.44999 85.11 9.33999 84.85 9.33999C84.59 9.33999 84.35 9.44999 84.18 9.61999C84.01 9.78999 83.9 10.03 83.9 10.29C83.9 10.55 84.01 10.79 84.18 10.96C84.35 11.13 84.59 11.24 84.85 11.24C85.11 11.24 85.35 11.13 85.52 10.96C85.69 10.79 85.8 10.55 85.8 10.29C85.8 10.03 85.69 9.78999 85.52 9.61999ZM84.85 7.12999C85.72 7.12999 86.51 7.47999 87.08 8.04999C87.65 8.61999 88 9.40999 88 10.28C88 11.15 87.65 11.94 87.08 12.51C86.51 13.08 85.72 13.43 84.85 13.43C83.98 13.43 83.19 13.08 82.62 12.51C82.05 11.94 81.7 11.15 81.7 10.28C81.7 9.40999 82.05 8.61999 82.62 8.04999C83.19 7.47999 83.98 7.12999 84.85 7.12999ZM73.07 20.66C72.89 21.95 72.52 22.92 72.04 23.68C72.58 23.51 73.12 23.3 73.65 23.08C75.29 22.38 76.82 21.44 77.94 20.31C78.13 20.11 78.38 20 78.64 19.98C82.04 19.7 85.05 18.48 87.19 16.68C89.23 14.97 90.47 12.73 90.47 10.29C90.47 7.65999 89.02 5.25999 86.69 3.49999C84.26 1.66999 80.89 0.549988 77.14 0.549988C73.39 0.549988 70.02 1.67999 67.6 3.49999C65.26 5.25999 63.82 7.65999 63.82 10.29C63.82 12.28 64.65 14.14 66.06 15.69C67.57 17.34 69.73 18.63 72.29 19.37C72.85 19.53 73.19 20.1 73.07 20.67V20.66Z"
					fill="currentColor"
				/>
			</svg>
		</div>
		<div class="form-container">
			<div class="contact-information-container">
		<div>
		<h3>Address</h3>
		<p>
		1234 Main St, Anytown, USA
		</p>
	</div>
	<div>
		<h3>Phone</h3>
		<p>
		(123) 456-7890
		</p>
	</div>
	<div>
		<h3>Email</h3>
		<p>godotgurus@gmail.com
		</p>
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
		align-self: baseline;
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
	.banner {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 16rem;
		background-color: var(--bg-color-banner);
	}
	.banner-icon {
		display: block;
	}
	@media (max-width: 1000px) {
		.banner-icon {
			display: none;
		}
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
		gap: 0.4rem;
		margin-top: 2rem;
	}
</style>
