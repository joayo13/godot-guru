<script>
	// Add any script logic here if needed
</script>

<div class="plans-container">
	<div class="plan">
		<div class="plan-title">Basic Plan</div>
		<div class="plan-price">$50</div>
		<ul class="plan-features">
			<li>50+ hours video lessons.</li>
			<li>50 interactive lessons.</li>
		</ul>
	</div>
	<div class="plan">
		<div class="plan-title">Standard Plan</div>
		<div class="plan-price">$100</div>
		<ul class="plan-features">
			<li>50+ hours video lessons.</li>
			<li>125 interactive lessons.</li>
		</ul>
	</div>
	<div class="plan">
		<div class="plan-title">Premium Plan</div>
		<div class="plan-price">$200</div>
		<ul class="plan-features">
			<li>All previous benefits.</li>
			<li>1-on-1 mentoring</li>
		</ul>
	</div>
</div>

<style>
	.plans-container {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 1rem;
		z-index: 1;
		padding-top: 2rem;
		padding-bottom: 2rem;
		padding-left: 1rem;
		padding-right: 1rem;
		max-width: 50rem;
		margin-left: auto;
		margin-right: auto;
		position: relative;
	}
	@media (max-width: 768px) {
		.plans-container {
			flex-direction: column;
		}
		.plan {
			min-width: 100%;
		}
	}

	.plan {
		border-radius: 1rem;
		background-color: var(--bg-color-nav);
		padding: 1rem;
		flex: 1;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
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
