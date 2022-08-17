<script>
	import Data from '/Users/lucianoinfanti/hangultest/src/data/data.json';
	
	// export let choosenQuestion = Math.round(Math.random() * Data.length)
	export let x;
</script>

<main>
		<h1 class="title">{Data[x].character}</h1>
</main>

<style>
	h1 {
		margin-block-start: 0.5em;
		margin-block-end: 0em;
	}
.title{
		font-size: 250px;		
	}
	
</style>