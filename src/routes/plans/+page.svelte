<script>
    import { onMount } from 'svelte';
    import { loadStripe } from '@stripe/stripe-js';
  
    // @ts-ignore
    let stripe;
  
    onMount(async () => {
      stripe = await loadStripe(import.meta.env.VITE_STRIPE_PUBLISHABLE_KEY);
    });
  
    const handleCheckout = async () => {
      // @ts-ignore
      const { error } = await stripe.redirectToCheckout({
        lineItems: [
          { price: import.meta.env.VITE_STRIPE_PRICE_ID, quantity: 1 }
        ],
        mode: 'payment',
        successUrl: window.location.origin + '/success',
        cancelUrl: window.location.origin + '/cancel',
      });
  
      if (error) {
        console.error('Error:', error);
      }
    };
  </script>
  
  <button style="margin-top: 20rem;" on:click={handleCheckout}>Checkout</button>