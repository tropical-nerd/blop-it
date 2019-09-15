<script>
	const actions = ['Blop It!', 'Smush It!', 'Crack It!', 'Smack It!'];
	
	let currentAction = '';
	let round = 0;
	let commandList = [];
	let note = ''
	let gamePaused = false;
	
	function actionClick(index) {
		if (round === 0 || commandList.length === 0) {return}
		
		if (index === commandList[0]) {
			commandList.shift();
			commandList = commandList
			 
			if (commandList.length === 0) {
				note = 'Got it!';
				newRound();
			}
		} else {
			note= 'Missed it! You gotta start over';
			newGame();
		}
	}
	
	function newGame() {
		round = 0;
	}

	function newRound() {
		note = '';
		round += 1;
		makeCommandList(round);
	}
	
	function makeCommandList(count) {
		commandList = [];
		
		for (let i = 0; i < count; i++) {
			commandList = commandList.concat([parseInt(Math.random() * 4, 10)])
		}
	} 
	
	//function togglePaused() {
	//	!gamePaused ? gamePaused = true : gamePaused = false;
	//}
	
</script>

<style>
	.body {
		background-color: #e0e0e0;
	}
	.action-btn {
		text-transform: uppercase;
		font-weight: 600;
		padding: .75em 1em;
		border-radius: .5em;
		border: none;
		color: #FFF;
		font-family: Impact;
		font-size: 1.5em;
	}
	.action-btn + .action-btn {margin-left: .5em}
	.action-btn-0 {background-color: #FF33FF}
	.action-btn-1 {background-color: #3355FF}
	.action-btn-2 {background-color: #FFFF33; color: #111111}
	.action-btn-3 {background-color: #33FFFF; color: #111111}

	.round-counter {
		background-color: green;
		color: white;
		font-family: Impact;
		display: flex;
		flex-direction: column;
		width: 6em;
		text-align: center;
		padding-top: .5em;
	}
	.round-number {
		font-size: 3em;
		margin-bottom: .125em;
	}
	.start-button {
		display: block;
		margin-bottom: 0;
	}
</style>

<h1>Blop It!</h1>

	<aside class="round-counter">
		Round<span class="round-number">{round}</span>
		{#if !round}
			<button class="start-button" on:click={() => newRound()}>
				Start Game
			</button>
		{/if}
	</aside>

<ul>
	{#each commandList as actionIndex}
		<li>{actions[actionIndex]}</li>
	{/each}
</ul>

{#each actions as action, index}
	<button class={'action-btn action-btn-' + (index)} on:click="{() => actionClick(index)}">
		{action}
	</button>
{/each}

<p class="note">
	{note}
</p>


