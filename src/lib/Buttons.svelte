<script>
	import Data from '/Users/lucianoinfanti/hangultest/src/data/data.json';
	import Question from '/Users/lucianoinfanti/hangultest/src/lib/Question.svelte';
	import Header from './Header.svelte';

	let counter = 0;
	let current = 'default';
	let tapCount = 0;

	let randomArray = [];
	let finalArray = [];
	let tempVar = [];

	let rightAnswer = Math.floor(Math.random() * 5); 
	console.log('rightAnswer ANTES de clicar é:' + rightAnswer);

	randomizeButtonAnswer();

	function randomizeButtonAnswer() {
		if (finalArray.length === 0) {
			for (let i=0; i < 5; i++){
				let randomNumber = Math.floor(Math.random() * Data.length); 
					if (!randomArray.includes(randomNumber)) {
						randomArray.push(randomNumber);	
					} else {
						i--;
					}
				}
		} else {
			randomArray = [];
			for (let i=0; i < 5; i++){
				let randomNumber = Math.floor(Math.random() * Data.length); 
					if (!randomArray.includes(randomNumber)) {
						randomArray.push(randomNumber);	
					} else {
						i--;
					}
				}
		}
		finalArray = randomArray.sort(() => Math.random() - 0.5);
		console.log('finalArray é: ' + finalArray);
	}

	function generateNextRightAnswerIndex() {
		tempVar = finalArray[rightAnswer]; // CHECAR O VALOR DO RIGHT ANSWOER NO DATA.JSON NAO A POSICAO! 
		console.log('tempVar é:' + tempVar);
		rightAnswer = Math.floor(Math.random() * 5); // ta só gerando 1 numero de 0 a 4 e n mudando a parada PODIA SER FUNCAO
		console.log('rightAnswer DEPOIS de clicar é:' + rightAnswer);
		if (finalArray[rightAnswer] === tempVar){
			rightAnswer = Math.floor(Math.random() * 5);
		}
	}

	function checkAnswer(value) {	
			if ( finalArray[value] === finalArray[rightAnswer] ) {
				randomizeButtonAnswer();
				generateNextRightAnswerIndex();
				const count = counter++;
			} else {
				tapCount++;	
			}
	}

	function reset() {
		counter = 0;
		tapCount = 0;
		randomizeButtonAnswer();
		generateNextRightAnswerIndex();
		current = 'default';
	}

	function colorizeWrong(value) {
		if (value != rightAnswer) {
			let whichIndex = randomOrder.indexOf(value);
			let whichIndexString = (whichIndex).toString();
			current = "wrong"+whichIndexString;
		}
	}
 </script>


<main>
	<div class="content-wrapper">
		<Header tapCount={tapCount} counter={counter}/>
		<div>	
				
			<Question x={randomArray[rightAnswer]}/>
			
			<div class="button-wrapper">
				<button  class:wrong0="{current === 'wrong0'}" on:click="{() => current = 'default'}" on:click={() => checkAnswer(0)}> 
					{Data[finalArray[0]].char_id} 
				</button>

				<button class:wrong1="{current === 'wrong1'}" on:click={() => checkAnswer(1)}> 
					{Data[finalArray[1]].char_id} 
				</button>

				<button class:wrong2="{current === 'wrong2'}" on:click={() => checkAnswer(2)}> 
					{Data[finalArray[2]].char_id} 
				</button>
				
				<button class:wrong3="{current === 'wrong3'}" on:click={() => checkAnswer(3)}> 
					{Data[finalArray[3]].char_id} 
				</button>

				<button class:wrong4="{current === 'wrong4'}" on:click={() => checkAnswer(4)}> 
					{Data[finalArray[4]].char_id} 
				</button>
			</div>
		</div>
		
		<button class="reset" on:click={() => reset()}> Reset </button>
	</div>
</main>


<style>
	.content-wrapper{
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		width: 100vh;
		margin: 0 auto;
		text-align: center;
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
		color: #3F3F3F;
		font-size: 16px;
		border: none;
	}
</style>


<!-- 
to do
* Adicionar variantes faltantes de hangul
* Impedir de repetir a mesma coisa nos botoes
* Impedir de randomizar o msmo exercicio 2x seguidas
* Filtro -->



	