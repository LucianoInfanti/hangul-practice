<script>
	import Data from '/Users/lucianoinfanti/hangultest/src/data/data.json';
	
	// export let choosenQuestion = Math.round(Math.random() * Data.length)
	export let x;
</script>

<main>
	<h1 class="title">{Data[x].character}</h1>
</main>

<style>
	.title{
		font-size: 128px;
	}
</style>
	<!-- <ul>
		{#each Data as {character}}
			<li>{character}</li>
		{/each}
	</ul>  -->