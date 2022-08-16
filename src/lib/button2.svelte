<script>
	import Data from '/Users/lucianoinfanti/hangultest/src/data/data.json';
	import Question from '/Users/lucianoinfanti/hangultest/src/lib/Question.svelte';

	let answer = false;
	let counter = 0;
	let current = 'default';
	let tapCount = 0;

	let randomArray = [];
	let finalArray = [];
	r();

	let rightAnswer = Math.floor(Math.random() * (6 - 0) + 0);

	function r() {
	for (let i=0; i < 5; i++){
		let randomNumber = Math.floor(Math.random() * Data.length);
			if (!randomArray.includes(randomNumber)) {
				randomArray.push(randomNumber);	
			} else {
				i--;
			}
		}
	finalArray = randomArray.sort(() => Math.random() - 0.5);

	}

	console.log(randomArray);
	console.log(rightAnswer);
	console.log(randomArray[rightAnswer]);

function checkAnswer(value) {	
		if ( randomArray[value] === randomArray[rightAnswer] ) {
			const count = counter++;
		} else {
			answer = false;
			tapCount++;		}
	}

	function reset() {
		counter = 0;
		tapCount = 0;
		current = 'default';
	}

	// function colorizeWrong(value) {
	// 	if (value != rightAnswer) {
	// 		let whichIndex = randomOrder.indexOf(value);
	// 		let whichIndexString = (whichIndex).toString();
	// 		current = "wrong"+whichIndexString;
	// 	}
	// }
 </script>


<main>
	<Question x={randomArray[rightAnswer]}/>

	<p>Correct {counter} · Incorrect {tapCount} </p>

	<div>
		<button class:wrong="{current === 'wrong0'}" on:click="{() => current = 'default'}" on:click={() => checkAnswer(finalArray[0])}> 
			{Data[finalArray[0]].char_id}
		</button>

		<button class:wrong="{current === 'wrong1'}" on:click={() => checkAnswer(finalArray[1])}> 
			{Data[finalArray[1]].char_id} 
		</button>

		<button class:wrong="{current === 'wrong2'}" on:click={() => checkAnswer(finalArray[2])}> 
			{Data[finalArray[2]].char_id} 
		</button>
		
		<button class:wrong="{current === 'wrong3'}" on:click={() => checkAnswer(finalArray[3])}> 
			{Data[finalArray[3]].char_id} 
		</button>

		<button class:wrong="{current === 'wrong4'}" on:click={() => checkAnswer(finalArray[4])}> 
			{Data[finalArray[4]].char_id} 
		</button>
	</div>

	<button class="reset" on:click={() => reset()}> Reset </button>
</main>


<style>
	.wrong {
		background-color: red;
	}

	.wrong0 {
		background-color: red;
	}
	.wrong1 {
		background-color: red;
	}

	.wrong2 {
		background-color: red;
	}
	.wrong3 {
		background-color: red;
	}
	.wrong4 {
		background-color: red;
	}
	.reset{
		background-color: #242424;
		font-size: 10px;
		margin-top: 24px;
	}
</style>


<!-- 
to do
* Adicionar variantes faltantes de hangul
* Impedir de repetir a mesma coisa nos botoes
* Impedir de randomizar o msmo exercicio 2x seguidas
* Filtro -->



	