<script>
	import Button from '@smui/button';
</script>

<main>
	<section class="head-section">
		<div class="banner">
			<h2>Transaction Cancelled</h2>
		</div>
		<div class="text-section">
			<p
				>"Never give up on something that you can’t go a day without thinking about." - Winston
				Churchill</p
			>
			<p>
				Your transaction has been cancelled. While we understand your decision, we hope that you
				reconsider in the future. Happy Gaming.
			</p>
			<p>-The Godot Guru Team</p>
			<Button href="/" style="text-decoration: underline; margin-bottom: 30rem;"
				>Return to home</Button
			>
		</div>
	</section>
</main>

<style>
	p {
		line-height: 1.5rem;
		font-size: 1.2rem;
	}
	h2 {
		font-family: 'Montserrat', sans-serif;
		font-size: 3rem;
		
		padding-left: 1rem;
	}
	main {
		padding-top: 4rem;
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
		background-color: var(--bg-color-page);
		color: var(--text-color);
		width: 100%;
	}
	section {
		padding-bottom: 2rem;
	}
	.head-section {
		margin-left: auto;
		margin-right: auto;
	}
	.text-section {
		margin-left: auto;
		margin-right: auto;
		max-width: 60rem;
		padding-top: 2rem;
		padding-left: 1rem;
		padding-right: 1rem;
	}
	.banner {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 16rem;
		background-color: var(--bg-color-banner);
	}
</style>
