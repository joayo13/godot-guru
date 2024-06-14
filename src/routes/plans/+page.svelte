<script>
	import { onMount } from 'svelte';
	import { loadStripe } from '@stripe/stripe-js';

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
	const handleCheckoutStandardPlus = async () => {
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

<button style="margin-top: 20rem;" on:click={handleCheckoutBasic}>Checkout Basic</button>
<button style="margin-top: 20rem;" on:click={handleCheckoutStandard}>Checkout Standard</button>
<button style="margin-top: 20rem;" on:click={handleCheckoutStandardPlus}>Checkout Premium</button>
