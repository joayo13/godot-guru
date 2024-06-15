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
	<section class="head-section">
		<div class="banner">
			<h2 style="margin-left: 1rem;">Plans & Pricing</h2>
			<svg
				style="margin-top: 1rem;"
				class="banner-icon"
				width="200"
				height="150"
				viewBox="0 0 101 76"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
			>
				<path
					d="M100.02 40.195V61.257C100.02 61.6164 99.727 61.9132 99.3637 61.9132H76.0587C75.6955 61.9132 75.4025 61.6203 75.4025 61.257L75.3986 40.195C75.3986 39.6364 75.8009 38.82 76.2423 38.4802L85.4493 31.3943L85.4962 31.3552L87.0392 30.1677C87.2033 30.0388 87.4494 29.9646 87.7072 29.9646C87.965 29.9646 88.2072 30.0388 88.3712 30.1677L89.4689 31.0115C88.9963 31.9646 88.3322 32.5271 87.7033 32.5271C87.258 32.5271 86.8948 32.8864 86.8948 33.3357C86.8948 33.781 87.2541 34.1442 87.7033 34.1442C88.9455 34.1442 90.0353 33.3278 90.7697 32.0154L99.1681 38.4762C99.6135 38.82 100.02 39.6364 100.02 40.195ZM91.8833 45.5036C92.3286 45.5036 92.6919 45.1442 92.6919 44.695C92.6919 42.6833 90.8833 41.0075 88.52 40.695V38.6755C88.52 38.2302 88.1606 37.8669 87.7114 37.8669C87.2661 37.8669 86.9067 38.2263 86.9067 38.6755V40.695C84.5434 41.0075 82.7348 42.6833 82.7348 44.695C82.7348 46.9333 84.9692 48.7497 87.7114 48.7497C89.5708 48.7497 91.0786 49.8435 91.0786 51.1911C91.0786 52.5387 89.5708 53.6325 87.7114 53.6325C85.8559 53.6325 84.3481 52.5387 84.3481 51.1911C84.3481 50.7458 83.9887 50.3825 83.5395 50.3825C83.0942 50.3825 82.7309 50.7419 82.7309 51.1911C82.7309 53.2028 84.5395 54.8786 86.9028 55.1911V57.2106C86.9028 57.6559 87.2661 58.0192 87.7075 58.0192C88.1528 58.0192 88.5161 57.6598 88.5161 57.2106V55.1911C90.8794 54.8786 92.688 53.2028 92.688 51.1911C92.688 48.9528 90.4536 47.1364 87.7075 47.1364C85.852 47.1364 84.3442 46.0426 84.3442 44.695C84.3442 43.3512 85.852 42.2536 87.7075 42.2536C89.5669 42.2536 91.0747 43.3513 91.0747 44.695C91.0747 45.1403 91.438 45.5036 91.8833 45.5036Z"
					fill="currentColor"
				/>
				<path
					d="M87.715 0.772949C94.5002 0.772949 100.024 6.29635 100.024 13.082C100.024 18.6484 96.3092 23.363 91.231 24.879C90.5435 23.0079 89.2427 21.7734 87.7193 21.7734C87.274 21.7734 86.9107 22.1328 86.9107 22.582C86.9107 23.0273 87.2701 23.3906 87.7193 23.3906C88.4185 23.3906 89.1646 24.0899 89.6412 25.2461C89.0162 25.3438 88.3756 25.3946 87.7193 25.3946C86.7662 25.3946 85.8365 25.2852 84.9459 25.0782C79.4889 23.8165 75.4107 18.9141 75.4107 13.0862C75.4029 6.29706 80.9263 0.774159 87.7157 0.774159L87.715 0.772949Z"
					fill="currentColor"
				/>
				<path
					d="M67.82 69.5229H80.523C80.1558 72.7299 77.6402 75.2221 74.5972 75.2221H24.5702C26.2343 73.894 27.371 71.851 27.5858 69.5229H67.82Z"
					fill="currentColor"
				/>
				<path d="M21.676 55.188H27.0822V60.5942H21.676V55.188Z" fill="currentColor" />
				<path d="M21.676 41.73H27.0822V47.1362H21.676V41.73Z" fill="currentColor" />
				<path d="M21.676 28.277H27.0822V33.6832H21.676V28.277Z" fill="currentColor" />
				<path d="M21.676 14.816H27.0822V20.2222H21.676V14.816Z" fill="currentColor" />
				<path
					d="M67.016 7.28098V67.91H26.813C26.3677 67.91 26.0044 68.2694 26.0044 68.7186C26.0044 72.2381 23.4302 75.1131 20.2232 75.2225C16.7271 75.117 13.9185 72.2381 13.9185 68.7186L13.9224 7.28057C13.9224 4.62037 12.6372 2.25717 10.6568 0.772766H60.5088C64.0947 0.772766 67.016 3.69508 67.016 7.28098ZM58.6371 14.0115C58.6371 13.5662 58.2777 13.2029 57.8285 13.2029H33.6445C33.1992 13.2029 32.8359 13.5623 32.8359 14.0115C32.8359 14.4568 33.1953 14.8201 33.6445 14.8201H57.8285C58.2738 14.8162 58.6371 14.4568 58.6371 14.0115ZM58.6371 27.4685C58.6371 27.0232 58.2777 26.6599 57.8285 26.6599L33.6445 26.6638C33.1992 26.6638 32.8359 27.0232 32.8359 27.4724C32.8359 27.9177 33.1953 28.281 33.6445 28.281H57.8285C58.2738 28.2771 58.6371 27.9138 58.6371 27.4685ZM58.6371 40.9255C58.6371 40.4802 58.2777 40.1169 57.8285 40.1169H33.6445C33.1992 40.1169 32.8359 40.4763 32.8359 40.9255C32.8359 41.3708 33.1953 41.7341 33.6445 41.7341H57.8285C58.2738 41.7302 58.6371 41.3708 58.6371 40.9255ZM58.6371 54.3825C58.6371 53.9372 58.2777 53.5739 57.8285 53.5739H33.6445C33.1992 53.5739 32.8359 53.9333 32.8359 54.3825C32.8359 54.8278 33.1953 55.1911 33.6445 55.1911H57.8285C58.2738 55.1872 58.6371 54.8278 58.6371 54.3825ZM50.7387 17.5235C50.7387 17.0782 50.3793 16.7149 49.9301 16.7149H33.6451C33.1998 16.7149 32.8365 17.0743 32.8365 17.5235C32.8365 17.9688 33.1959 18.3321 33.6451 18.3321H49.9301C50.3754 18.3282 50.7387 17.9649 50.7387 17.5235ZM50.7387 30.9765C50.7387 30.5312 50.3793 30.1679 49.9301 30.1679H33.6451C33.1998 30.1679 32.8365 30.5273 32.8365 30.9765C32.8365 31.4218 33.1959 31.7851 33.6451 31.7851H49.9301C50.3754 31.7851 50.7387 31.4257 50.7387 30.9765ZM50.7387 44.4375C50.7387 43.9922 50.3793 43.6289 49.9301 43.6289H33.6451C33.1998 43.6289 32.8365 43.9883 32.8365 44.4375C32.8365 44.8828 33.1959 45.2461 33.6451 45.2461H49.9301C50.3754 45.2422 50.7387 44.8828 50.7387 44.4375ZM50.7387 57.8905C50.7387 57.4452 50.3793 57.0819 49.9301 57.0819H33.6451C33.1998 57.0819 32.8365 57.4452 32.8365 57.8905C32.8365 58.3358 33.1959 58.6991 33.6451 58.6991H49.9301C50.3754 58.6991 50.7387 58.3397 50.7387 57.8905ZM28.6997 61.4022V54.3788C28.6997 53.9335 28.3403 53.5702 27.8911 53.5702H20.8677C20.4224 53.5702 20.0591 53.9296 20.0591 54.3788V61.4022C20.0591 61.8475 20.4185 62.2108 20.8677 62.2108H27.8911C28.3403 62.2108 28.6997 61.8514 28.6997 61.4022ZM28.6997 47.9452V40.9257C28.6997 40.4804 28.3403 40.1171 27.8911 40.1171H20.8677C20.4224 40.1171 20.0591 40.4765 20.0591 40.9257V47.9452C20.0591 48.3905 20.4185 48.7538 20.8677 48.7538H27.8911C28.3403 48.7538 28.6997 48.3905 28.6997 47.9452ZM28.6997 34.4922V27.4688C28.6997 27.0235 28.3403 26.6602 27.8911 26.6602H20.8677C20.4224 26.6602 20.0591 27.0196 20.0591 27.4688V34.4922C20.0591 34.9375 20.4185 35.3008 20.8677 35.3008H27.8911C28.3403 35.2969 28.6997 34.9336 28.6997 34.4922ZM28.6997 21.0312V14.0078C28.6997 13.5625 28.3403 13.1992 27.8911 13.1992H20.8677C20.4224 13.1992 20.0591 13.5586 20.0591 14.0078V21.0312C20.0591 21.4765 20.4185 21.8398 20.8677 21.8398H27.8911C28.3403 21.8398 28.6997 21.4765 28.6997 21.0312Z"
					fill="currentColor"
				/>
				<path
					d="M12.258 6.47697H0.0239868C0.387267 3.29337 2.86779 0.816771 5.87949 0.777771C5.96933 0.777771 6.05527 0.781677 6.14511 0.785583C9.30531 0.949643 11.8713 3.37937 12.258 6.47697Z"
					fill="currentColor"
				/>
			</svg>
		</div>
		<div class="text-section">
			<em
				>"Don&apos;t be afraid to fail. Failure is often the best path to success." - John Romero</em
			>
			<p>With our plans it's a one-time-fee, and you'll own it for a lifetime.</p>
			<div class="plans-container">
				<div class="plan">
					<div class="plan-title">Basic Plan</div>
					<div class="plan-price">$50</div>
					<ul class="plan-features">
						<li>50+ hours video lessons.</li>
						<ul>
							<li>10 hours fundamentals</li>
							<li>10 hours game physics</li>
							<li>5 hours 3D graphics</li>
							<li>5 hours 2D graphics</li>
							<li>10 hours game design</li>
							<li>10 hours case studies</li>
						</ul>
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
						<ul>
							<li>10 hours fundamentals</li>
							<li>10 hours game physics</li>
							<li>5 hours 3D graphics</li>
							<li>5 hours 2D graphics</li>
							<li>10 hours game design</li>
							<li>10 hours case studies</li>
						</ul>
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
						<ul>
							<li>Career Advice</li>
							<li>Code Reviews</li>
							<li>Design Advice</li>
							<li>Pair Programming</li>
							<li>Troubleshooting</li>
							<li>General Questions</li>
						</ul>
					</ul>
					<Button on:click={handleCheckoutPremium} touch>
						<Label style="text-decoration: underline;">Purchase Premium</Label>
						<Icon class="material-icons">shopping_cart</Icon>
					</Button>
				</div>
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
		font-family: 'Montserrat', sans-serif;
		background-color: var(--bg-color-page);
		color: var(--text-color);
		width: 100%;
	}
	.head-section {
		margin-left: auto;
		margin-right: auto;
	}
	.text-section {
		max-width: 60rem;
		padding-top: 2rem;
		padding-left: 1rem;
		padding-right: 1rem;
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
	}
</style>
