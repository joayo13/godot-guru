<script lang="ts">
	import Textfield from '@smui/textfield';
	import CharacterCounter from '@smui/textfield/character-counter';
	import Button from '@smui/button';
	let valueA = '';
	let valueB = '';
	let valueC = '';
</script>

<main>
	<section class="head-section" style="max-width: 60rem;">
		<h2>Contact Form</h2>
		<form>
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
		</form>
	</section>
</main>

<style>
	h2 {
		font-size: 4rem;
		max-width: max-content;
		text-align: center;
		margin: 10px;
	}
	p {
		line-height: 1.5rem;
		font-size: 1.2em;
		text-align: center;
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
	section {
		padding: 1rem;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.head-section {
		margin-left: auto;
		margin-right: auto;
	}
	form {
		display: flex;
		flex-direction: column;
		gap: 2rem;
	}
</style>
