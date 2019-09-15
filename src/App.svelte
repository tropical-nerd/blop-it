<script>
	const actions = ['Blop It!', 'Smush It!', 'Crack It!', 'Smack It!'];
	const gameBoard = [
		
	];

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
		position: absolute;
		right: 1em;
	}
	.round-number {
		font-size: 3em;
		margin-bottom: .125em;
		
	}
	.start-button {
		display: block;
		margin-bottom: 0;
		border-radius: 0;
	}
	.game-board {
		width: 100%;
		height: 100%;
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

<svg class="game-board" xmlns="http://www.w3.org/2000/svg" width="800" height="600" viewBox="0 0 211.667 158.75">
	<g stroke="#000">
		<path class="zap-right" d="M119.447 43.715c-6.441-2.274-6.978-6.152-5.77-9.361 1.208-3.21 8.32-6.954 5.905-11.902-2.416-4.947-8.992-8.825-8.992-8.825s-4.965 1.337-7.246-1.873c-2.282-3.209-1.88-11.5 4.965-9.494 6.844 2.006 4.831 9.628 4.831 9.628s6.442 4.547 8.589 11.367c2.147 6.82 2.013 20.727-2.282 20.46z" fill="#ffbe00" stroke-width=".265"/>
		<g class="chunk">
			<path d="M62.264 109.144l21.553 23.092 27.71-16.763-19.842-20.355z" fill="#37c8ab"/>
			<path d="M111.528 115.473l-.403-17.955L97.14 79.753l-5.455 15.365z" fill="#00aad4"/>
			<path d="M91.685 95.118l-29.421 14.026 14.54-24.119 20.336-5.272z" fill="#80ffe6"/>
		</g>
		<path class="body" d="M178.405 94.494c4.157-21.545-71.438-73.705-81.643-63.5-10.205 10.205 40.443 40.066 31.75 58.964-8.694 18.9-108.101 38.932-106.59 49.515 1.513 10.584 135.694 7.56 156.483-44.979z" fill="#93aca7" stroke-width=".265"/>
		<path class="zap-left" d="M112.53 52.75c-4.026 5.953-16.683 1.324-28.764-9.259-12.081-10.582-10.93-21.164-11.506-23.81l-.575-2.646s-3.527 2.51-6.404-2.78c-1.747-3.978 1.768-7.42 4.762-6.672 2.994.748 5.468 2.095 4.817 5.238-.651 3.143-1.042 3.143-1.042 3.143s2.474 19.605 12.237 24.544 28.609.84 26.476 12.243z" fill="#ffbe00" stroke-width=".265"/>
		<path class= "plurp" d="M25.487 137.368c5.474 4.619 15.395 6.158 24.632 2.053 9.237-4.106 14.027-12.145 11.803-15.908-2.224-3.764-10.606-8.382-21.553-7.869-10.948.513-22.58 4.619-25.145 11.803-2.566 7.184 17.105 1.71 22.921-1.71 5.816-3.422 11.46-10.777 10.092-14.37-1.368-3.591-14.71-8.039-20.355-8.38-5.645-.343-15.908 2.052-13.513 6.841 2.394 4.79 11.46 3.592 14.881 1.54 3.421-2.053 8.895-6.33 7.185-9.58s-7.014-7.355-10.093-5.473c-3.079 1.882-2.394 2.395-.342 4.276 2.053 1.882 9.922 0 11.119-1.881 1.197-1.882 2.224-4.96-3.08-7.185-5.302-2.223-9.578.685-7.525 2.566 2.052 1.882 4.789 2.053 6.329 1.369 1.539-.685 5.986-5.987 2.736-8.382-3.25-2.395-6.67-1.197-6.329.342.343 1.54 8.211 4.105 10.777 2.566 2.566-1.54 5.303-4.79 4.105-6.5-1.197-1.71-5.987-4.277-5.987-4.277s3.935 3.935 3.25 5.303c-.684 1.369-1.026 4.96-3.42 4.277-2.396-.685-4.106.684-5.304-1.198-1.197-1.881 1.369-2.908 2.908-1.71 1.54 1.197.171 5.473-1.197 7.013s-3.25 6.842-6.671 4.96c-3.421-1.881-8.553-5.131-5.132-6.5 3.421-1.368 5.303-2.223 7.869-1.197 2.566 1.026 7.526 4.447 6.158 7.013-1.369 2.566.684 4.277-6.671 4.448-7.356.17-8.895-1.882-8.04-3.935.855-2.052 7.184-1.881 10.092.171 2.908 2.053 6.33.856 6.5 5.303.171 4.448-1.197 8.553-5.473 10.092-4.277 1.54-13.856 7.185-18.816 3.421-4.961-3.763-6.5-10.605-1.882-11.631 4.618-1.027 13.342-2.224 18.474-.342 5.132 1.881 5.816 1.881 9.408 5.473 3.592 3.593 4.447 8.895.513 12.145s-15.908 4.448-19.5 4.448c-3.592 0-7.698.17-8.04-2.908-.342-3.08 4.619-9.066 10.092-9.75 5.474-.685 10.948-2.053 15.395-1.369 4.448.684 15.909 1.369 18.645 3.08 2.737 1.71 3.593 10.263.514 13.341-3.08 3.08-27.37 10.777-29.422 10.606-2.053-.171-2.908-2.395-2.908-2.395z" fill="purple" stroke-width=".265"/>
		<g class="blop">
			<path d="M140.607 54.807c-17.009 12.85-21.167 20.032-20.789 29.482.378 9.45 1.134 15.119 7.182 19.654 6.048 4.536 9.827 10.584 14.741 12.474 4.914 1.89 15.12 4.913 22.679 1.89 7.56-3.024 12.095-5.67 17.009-13.23 4.913-7.56 6.425-12.473 6.425-18.898 0-6.426.378-13.23-4.914-16.253-5.291-3.024-11.717-10.584-16.253-13.23-4.535-2.645-13.607-5.291-17.008-4.157-3.402 1.134-5.67.756-9.072 2.268z" fill="maroon" stroke-width=".265"/>
			<path d="M148.923 60.854c-13.986 9.072-26.459 11.34-23.435 28.726 3.024 17.387 18.143 24.19 30.238 23.813 12.095-.378 26.837-2.646 27.97-22.3 1.134-19.656-8.315-24.947-15.875-28.349-7.56-3.402-12.473-4.158-18.898-1.89z" fill="#d40000" stroke-width=".265"/><path d="M128.53 77.333l4.983 19.5 8.825-5.266-8.683-3.132 2.99-5.978zm1.994 3.416l4.27 2.135-1.993 4.128zm2.562 9.536l6.69 1.566-5.552 2.704z" fill="#fff" stroke-width=".26458"/>
			<path d="M137.363 72.9l7.216 21.901 13.292-7.3-11.773 1.991z" fill="#fff" stroke-width=".265"/>
			<path d="M150.593 66.515l-4.84 15.373 14.092 5.266 6.12-11.53zm2.99 5.551l7.543 5.836-2.277 3.559-7.971-1.566z" fill="#f9f9f9" stroke-width=".26458"/>
			<path d="M166.82 67.654l.57 18.788 1.707-10.675 8.113-3.416zm.996 1.566l6.12 3.273-5.835 1.993z" fill="#fff" stroke-width=".26458"/>
			<path d="M151.732 97.402l1.708 13.523 3.558-.427zM149.882 95.267l23.058-7.828-9.11 7.117 2.847 15.372-5.693-14.518zM175.218 86.015s1.85 13.523 2.135 12.953c.284-.57.996-15.8.996-15.8zM177.068 100.819l-.854 3.273 1.85-1.28z" fill="#fff" stroke-width=".265"/>
		</g>
	</g>
</svg>

{#each actions as action, index}
	<button class={'action-btn action-btn-' + (index)} on:click="{() => actionClick(index)}">
		{action}
	</button>
{/each}

<p class="note">
	{note}
</p>


