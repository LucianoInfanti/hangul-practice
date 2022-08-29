<script>
	import Data from '../data/data.json';
	import Question from './Question.svelte';
	import Header from './Header.svelte';

	let counter = 0;
	let tapCount = 0;

	let current = 'default';

	let randomArray = [];
	let finalArray = [];

	let rightAnswer = Math.floor(Math.random() * 5); 

	randomizeButtonAnswer();

	function randomizeButtonAnswer() {
		let lastArray = randomArray;
		randomArray = [];
			for (let i=0; i < 5; i++){
				let randomNumber = Math.floor(Math.random() * Data.length); 
					if (!randomArray.includes(randomNumber) && !lastArray.includes(randomNumber)) {
						randomArray.push(randomNumber);	
					} else {
						i--;
					}
				}
		finalArray = randomArray.sort(() => Math.random() - 0.5);
	}

	function generateNextRightAnswerIndex() {
		let lastIndex = rightAnswer;
		rightAnswer = Math.floor(Math.random() *5);
		while(rightAnswer === lastIndex){
			rightAnswer = Math.floor(Math.random() * 5);
		}
	}

	function checkAnswer(value) {	
			colorizeWrong(finalArray[value]);
			if ( value === rightAnswer ) {
				randomizeButtonAnswer();
				generateNextRightAnswerIndex();
				const count = counter++;
				current = 'default';
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
		if (finalArray[value] != finalArray[rightAnswer]) {
			let whichIndex = finalArray.indexOf(value);
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
			
			<div class="parent">
				<!-- svelte-ignore a11y-mouse-events-have-key-events -->
				<button	
					class="child"
					class:wrong0="{current === 'wrong0'}" 
					on:click={() => checkAnswer(0)}> 
					<span>{Data[finalArray[0]].char_id}
					</span>
				</button>

				<!-- svelte-ignore a11y-mouse-events-have-key-events -->
				<button 
					class="child"
					class:wrong1="{current === 'wrong1'}" 
					on:click={() => checkAnswer(1)}> 
					<span >{Data[finalArray[1]].char_id}</span>
				</button>

				<!-- svelte-ignore a11y-mouse-events-have-key-events -->
				<button
					class="child"
					class:wrong2="{current === 'wrong2'}" 
					on:click={() => checkAnswer(2)}> 
					<span >{Data[finalArray[2]].char_id}</span></button>
				
				<!-- svelte-ignore a11y-mouse-events-have-key-events -->
				<button 
					class="child"
					class:wrong3="{current === 'wrong3'}" 
					on:click={() => checkAnswer(3)}> 
					<span>{Data[finalArray[3]].char_id}</span>
				</button>

				<!-- svelte-ignore a11y-mouse-events-have-key-events -->
				<button 
					class="child"
					class:wrong4="{current === 'wrong4'}" 
					on:click={() => checkAnswer(4)}> 
					<span>{Data[finalArray[4]].char_id}</span>
				</button>

			</div>
		</div>
		
		<button class="reset" on:click={() => reset()}> Reset </button>
	</div>
</main>


<style>
	.child{
		padding-bottom:8px;
		border-bottom: 0.5px solid #3F3F3F;
		min-width: 44px;
		transition: 0.4s;
	}

	.child:hover{
		border-bottom: 0.5px solid white;
	}

	.content-wrapper{
		display: flex;
		flex-direction: column;
		text-align: center;
	}

	.wrong0 {
		border-bottom: 0.5px solid #FF4C4D;
		color: #FF4C4D;
	}
	.wrong1 {
		border-bottom: 0.5px solid #FF4C4D;
		color: #FF4C4D;
	}

	.wrong2 {
		border-bottom: 0.5px solid #FF4C4D;
		color: #FF4C4D;
	}
	.wrong3 {
		border-bottom: 0.5px solid #FF4C4D;
		color: #FF4C4D;
	}
	.wrong4 {
		border-bottom: 0.5px solid #FF4C4D;
		color: #FF4C4D;
	}

	.reset{
		color: #3F3F3F;
		font-size: 14px;
		margin-top: 10%;
		margin-right: 0px;
		margin-bottom: 30px;
	}
</style>