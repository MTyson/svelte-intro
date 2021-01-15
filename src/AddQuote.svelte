<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  let author = "";
  let quote = "";
  function onAdd(author, quote){
    dispatch('quote', {
			author: author, quote: quote
		});
  }
</script>

<main>
	<div class="add-quote">
    <h2>New Quote</h2>
    <div>Author: <input bind:value={author} placeholder="Author"></div>
    <div>Quote: <input bind:value={quote} placeholder="Quote"></div>
    <button on:click={()=>{onAdd(author, quote)}}>Add It!</button>
  </div>
</main>

<style>
  .add-quote {
    border: solid lightgrey;
  }
</style>