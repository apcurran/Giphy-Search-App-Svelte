<script>

	let search = "";
	const apiUrl = 'https://api.giphy.com/v1/gifs/search?api_key=XEAkZeR976diLYKcNhMlxn8S9Uvbbfza&rating=pg&q=';
	let gifs = [];

	async function getGifs(event) {
		gifs = [];
		const giphyUrl = `${apiUrl}${search}`;
		const response = await fetch(giphyUrl);
		const data = await response.json();
		gifs = data.data.map(gif => gif.images.fixed_height.url)
	}

</script>

<style>

	* {
		padding: 0;
		margin: 0;
		box-sizing: border-box;
	}

	h1,
	input,
	button {
		font-family: 'Segoe UI', 'Roboto', arial, sans-serif;
		letter-spacing: .02em;
	}

	body {
		background-color: #fefefe;
	}

	.title {
		margin: 2rem;
		text-align: center;
		font-size: 2.1rem;
		font-weight: 500;
	}

	.form {
		display: flex;
		justify-content: center;
	}

	.form-field {
		width: 35rem;
		max-width: 90%;
		display: flex;
		margin-bottom: 6rem;
	}

	.form-field-input {
		flex-grow: 1;
		padding: .5rem;
		font-size: 1.05rem;
		border: .5px solid #c6c6c6;
		border-top-left-radius: 4px;
		border-bottom-left-radius: 4px;
	}

	.form-field-input::placeholder {
		color: #bbb;
	}

	.form-field-submit {
		padding: .75rem 2.5rem;
		text-transform: uppercase;
		letter-spacing: .08em;
		font-size: 1rem;
		cursor: pointer;
		border: none;
		border-top-right-radius: 4px;
		border-bottom-right-radius: 4px;

		color: #222;
		font-weight: 500;
		background-color: #9AE6B4;
	}

	.results {
		width: 75rem;
		max-width: 90%;
		margin: 0 auto;
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(275px, 1fr));
		grid-gap: 1.5rem;
		grid-auto-flow: dense;
	}

	.results-gif {
		width: 100%;
		border-radius: 4px;
		box-shadow: 0 5px 13px rgba(0, 0, 0, .25);
	}

</style>

<!-- HTML -->
<h1 class="title">Giphy API</h1>
<form on:submit|preventDefault={ getGifs } class="form">
	<div class="form-field">
		<input bind:value={search} type="text" class="form-field-input" id="search" placeholder="Search for gifs">
		<input type="submit" value="Get Gifs" class="form-field-submit">
	</div>
</form>
<main class="results">
	{#each gifs as gif}
		<img src={ gif } alt="Gif" class="results-gif">
	{/each}
</main>
