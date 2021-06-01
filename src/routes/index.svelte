<script>
	import successkid from 'images/jake-givens-iR8m2RRo-z4-unsplash.jpg';
	import Search from '../components/Search.svelte'
	let usernameInputField = '';
	let repositories = undefined;

	async function onSubmit() {
		const url = `https://api.github.com/users/${usernameInputField}/repos`;

		const response = await fetch(url);
		repositories = await response.json();
		console.log('loaded repositories', repositories)
	}
</script>

<style>
	h1, figure {
		text-align: center;
		margin: 0 auto;
	}

	h1 {
		font-size: 2.8em;
		text-transform: uppercase;
		font-weight: 700;
		margin: 0 0 0.5em 0;
	}

	figure {
		margin: 0 0 1em 0;
	}

	img {
		width: 100%;
		max-width: 1200px;
		margin: 0 0 1em 0;
	}

	p {
		margin: 1em;
	}

	@media (min-width: 480px) {
		h1 {
			font-size: 4em;
		}
	}

</style>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>

<h1>Svelte and Sapper</h1>

<figure>
	<img alt="Elapsed time photo of highway at night" src="{successkid}">
	<figcaption>Have fun with Sapper!</figcaption>
</figure>

<p><strong>Enter a github username to retrieve public repositories:</strong></p>
<main>
	<div class="gitsearch">
	<form on:submit|preventDefault={onSubmit}>
		<label for="username">GitHub username:</label>
		<input type="text" name="username" placeholder="jackfranklin" bind:value={usernameInputField}/>
		<button type="submit">Load repositories</button>
	</form>
	{#if repositories}
		<Search {repositories} />
	{/if}
	</div>
</main>
