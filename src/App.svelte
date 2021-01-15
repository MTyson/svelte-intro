<script>
  import AddQuote from './AddQuote.svelte';
	let name = "Infoworld2";
	let quotes = [
		{author:"Emerson", quote:"To be great is to be misunderstood."},
		{author:"James", quote:"The art of being wise is the art of knowing what to overlook."},
		{author:"Thoreau", quote:"That government is best which governs least."}
	];
	function click(author){	alert("hello from " + author); }
	function onAddQuote(event){ 
		quotes = [...quotes, {author:event.detail.author, quote:event.detail.quote}];
		console.log("quotes: " + quotes);
	}
	async function addRandom(){
		const res = await fetch("https://api.quotable.io/random");
		const json = await res.json();
		console.log(JSON.stringify(json));
		quotes = [...quotes, {author:json.author, quote:json.content}];
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<ul>
		{#each quotes as { quote, author }, i}
			<li on:click="{() => click(author)}">{i} - {quote}</li>		
		{/each}
  </ul>
	<AddQuote on:quote={onAddQuote}></AddQuote>
	<button on:click={addRandom}>Add Random Quote</button>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
	li:hover{
		cursor: pointer;
	}
</style>