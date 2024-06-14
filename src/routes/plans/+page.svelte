<script>
	import { onMount } from 'svelte';
	import { loadStripe } from '@stripe/stripe-js';
	import Button, { Label, Icon } from '@smui/button';

	// @ts-ignore
	let stripe;

	onMount(async () => {
		stripe = await loadStripe(import.meta.env.VITE_STRIPE_PUBLISHABLE_KEY);
	});
	const handleCheckoutBasic = async () => {
		// @ts-ignore
		const { error } = await stripe.redirectToCheckout({
			lineItems: [{ price: import.meta.env.VITE_STRIPE_PRICE_ID_BASIC, quantity: 1 }],
			mode: 'payment',
			successUrl: window.location.origin + '/success',
			cancelUrl: window.location.origin + '/cancel'
		});

		if (error) {
			console.error('Error:', error);
		}
	};

	// @ts-ignore
	const handleCheckoutStandard = async () => {
		// @ts-ignore
		const { error } = await stripe.redirectToCheckout({
			lineItems: [{ price: import.meta.env.VITE_STRIPE_PRICE_ID_STANDARD, quantity: 1 }],
			mode: 'payment',
			successUrl: window.location.origin + '/success',
			cancelUrl: window.location.origin + '/cancel'
		});

		if (error) {
			console.error('Error:', error);
		}
	};
	const handleCheckoutPremium = async () => {
		// @ts-ignore
		const { error } = await stripe.redirectToCheckout({
			lineItems: [{ price: import.meta.env.VITE_STRIPE_PRICE_ID_PREMIUM, quantity: 1 }],
			mode: 'payment',
			successUrl: window.location.origin + '/success',
			cancelUrl: window.location.origin + '/cancel'
		});

		if (error) {
			console.error('Error:', error);
		}
	};
</script>

<main>
	<section class="head-section" style="max-width: 60rem;">
		<h2>Plans & Pricing</h2>
		<em>"Don&apos;t be afraid to fail. Failure is often the best path to success." - John Romero</em
		>
		<p>With our plans it's a one-time-fee, and you'll own it for a lifetime.</p>
		<div class="plans-container">
			<div class="plan">
				<div class="plan-title">Basic Plan</div>
				<div class="plan-price">$50</div>
				<ul class="plan-features">
					<li>50+ hours video lessons.</li>
					<li>50 interactive lessons.</li>
				</ul>
				<Button on:click={handleCheckoutBasic} touch>
					<Label style="text-decoration: underline;">Purchase Basic</Label>
					<Icon class="material-icons">shopping_cart</Icon>
				</Button>
			</div>
			<div class="plan">
				<div class="plan-title">Standard Plan</div>
				<div class="plan-price">$100</div>
				<ul class="plan-features">
					<li>50+ hours video lessons.</li>
					<li>125 interactive lessons.</li>
				</ul>
				<Button on:click={handleCheckoutStandard} touch>
					<Label style="text-decoration: underline;">Purchase Standard</Label>
					<Icon class="material-icons">shopping_cart</Icon>
				</Button>
			</div>
			<div class="plan">
				<div class="plan-title">Premium Plan</div>
				<div class="plan-price">$200</div>
				<ul class="plan-features">
					<li>All benefits of previous plans.</li>
					<li>1-on-1 mentoring</li>
				</ul>
				<Button on:click={handleCheckoutPremium} touch>
					<Label style="text-decoration: underline;">Purchase Premium</Label>
					<Icon class="material-icons">shopping_cart</Icon>
				</Button>
			</div>
		</div>
	</section>
</main>

<style>
	h2 {
		font-size: 4rem;
		max-width: max-content;
	}
	p {
		line-height: 1.5rem;
		font-size: 1.2em;
	}
	em {
		line-height: 1.5rem;
		font-size: 1.2em;
	}
	main {
		padding-top: 4rem;
    padding-bottom: 4rem;
		font-family: 'Montserrat', sans-serif;
		background-color: var(--bg-color-page);
		color: var(--text-color);
		width: 100%;
	}
	section {
		padding: 1rem;
	}
	.head-section {
		margin-left: auto;
		margin-right: auto;
	}
	.plans-container {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 1rem;
		z-index: 1;
		padding: 2rem;
		position: relative;
	}
	@media (max-width: 1000px) {
		.plans-container {
			flex-direction: column;
		}
	}

	.plan {
		border-radius: 1rem;
		background-color: var(--bg-color-nav);
		padding: 20px;
		margin: 10px;
		flex: 1;
		min-width: 250px;
		max-width: 300px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		transition:
			transform 0.3s,
			box-shadow 0.3s;
	}

	.plan-title {
		font-size: 1.5em;
		margin-bottom: 10px;
	}

	.plan-price {
		font-size: 1.2em;
		margin-bottom: 20px;
	}

	.plan-features {
		list-style: none;
		padding: 0;
		margin: 0;
	}

	.plan-features li {
		margin-bottom: 10px;
		margin-left: 15px;
		list-style: disc;
	}
</style>
