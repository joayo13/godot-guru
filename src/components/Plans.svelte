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
			<li>All benefits of previous plans.</li>
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
