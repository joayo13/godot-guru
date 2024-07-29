<script lang="ts">
	import { onMount } from 'svelte';
	let imageLoaded = false;
	let reviewImage: HTMLImageElement;
	onMount(() => {
		if (reviewImage && reviewImage.complete !== undefined) {
			// Check if the image is already loaded
			handleImageLoad(); // If loaded, update the imageLoaded state
		}
	});

	function handleImageLoad() {
		imageLoaded = true;
	}
</script>

<div class="reviews">
	<div class="review-card">
		<div class="image-container">
			{#if !imageLoaded}
				<img class="skeleton-image" src="jordanlowres.jpg" alt="loading..." />
			{/if}
			<img
				class="review-card-image"
				src="jordan.jpg"
				alt="jordan t."
				bind:this={reviewImage}
				on:load={() => (imageLoaded = true)}
				style="display: {imageLoaded ? 'block' : 'none'}"
			/>
		</div>
		<i>
			"This platform has been great for me. The lessons are well-structured and easy to follow, making
			complex game development concepts accessible even for beginners. The instructors are
			knowledgeable and always willing to help. I've already created my first game!" <b class="jordant">&nbsp;- Jordan T.</b>
		</i>
	</div>
</div>

<style>
	@media (max-width: 768px) {
		.review-card {
			flex-direction: column;
		}
		.jordant {
			display: block;
			line-height: 2rem;
		}
	}
	.jordant {
		font-size: 1.2rem;
		font-style: normal;
		font-weight: normal;
	}
	.reviews {
		position: relative;
		display: flex;
		flex-direction: column;
		margin-left: auto;
		margin-right: auto;
		max-width: 50rem;
		line-height: 1.5rem;
	}
	.review-card {
		background-color: var(--bg-color-nav);
		border-radius: 1rem;
		padding: 1rem;
		margin-top: 1rem;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		display: flex;
		gap: 1rem;
		align-items: center;
	}

	.review-card-image {
		border-radius: 50%;
		width: 6rem;
		height: 6rem;
		object-fit: cover;
	}
	.skeleton-image {
		border-radius: 50%;
		width: 6rem;
		height: 6rem;
		background-color: var(--bg-color-banner);
		filter: blur(5px);
	}
	@keyframes rotate {
		from {
			transform: rotate(0deg);
		}
		to {
			transform: rotate(360deg);
		}
	}
</style>
