<script>
	import Data from '/Users/lucianoinfanti/hangultest/src/data/data.json';
	import Question from '/Users/lucianoinfanti/hangultest/src/lib/Question.svelte';

	let counter = 0;
	let current = 'default';
	let tapCount = 0;

	let randomArray = [];
	let finalArray = [];
	let tempVar = 0;
	r();

	let rightAnswer = Math.floor(Math.random() * 5);

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

	function generateRightAnswer() {
		tempVar = rightAnswer;
		rightAnswer = Math.floor(Math.random() * 5);
		if (rightAnswer === tempVar){
			rightAnswer = Math.floor(Math.random() * 5);
		}
	}

	function checkAnswer(value) {	
			if ( finalArray[value] === randomArray[rightAnswer] ) {
				current = 'default';
				r();
				generateRightAnswer();
				const count = counter++;
			} else {
				tapCount++;	
			}
	}

	function reset() {
		counter = 0;
		tapCount = 0;
		r();
		generateRightAnswer();
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
		<button class:wrong="{current === 'wrong0'}" on:click="{() => current = 'default'}" on:click={() => checkAnswer(0)}> 
			{Data[finalArray[0]].char_id}
		</button>

		<button class:wrong="{current === 'wrong1'}" on:click={() => checkAnswer(1)}> 
			{Data[finalArray[1]].char_id} 
		</button>

		<button class:wrong="{current === 'wrong2'}" on:click={() => checkAnswer(2)}> 
			{Data[finalArray[2]].char_id} 
		</button>
		
		<button class:wrong="{current === 'wrong3'}" on:click={() => checkAnswer(3)}> 
			{Data[finalArray[3]].char_id} 
		</button>

		<button class:wrong="{current === 'wrong4'}" on:click={() => checkAnswer(4)}> 
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



	