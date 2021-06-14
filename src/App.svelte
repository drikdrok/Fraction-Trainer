<script>

	let numeratorLists = [
		[1], //Easy
		[1, 2, 3, 4, 5, 6], // Medium
		[1, 2, 3, 4, 5, 6, 7,8, 9, 10, 11, 12], // Hard
	];
	let denominatorLists = [
		[2, 3, 4, 5, 10], //Easy
		[2, 3, 4, 5, 6, 8, 9, 10], // Medium
		[3, 5, 6, 7, 8, 9, 10, 11, 12], // Hard
	]



	let numerator;
	let denominator;

	let difficulty = 1;

	let completed = 0;
	let correct = 0;

	let input;

	let showExplanation = true;

	function submitQuestion(){
		if (input == (numerator / denominator * 100).toFixed(2))
			correct++

		completed++;

		input = "";


		newQuestion();
	}

	function newQuestion(){
		denominator = denominatorLists[difficulty][rand(0, denominatorLists[difficulty].length)];
		
		do {
			numerator = numeratorLists[difficulty][rand(0, numeratorLists[difficulty].length)];
		} while (numerator > denominator)
		
	}

	function rand(min, max) {
		return Math.floor(Math.random() * (max - min) ) + min;
	}

	newQuestion();

</script>


<div id = "content">
	<div id = "center">
		<div id="head">
			<h2>Correct: {correct}/{completed}</h2>
			<h1>Fractions</h1>
			<h2>Difficulty: {difficulty}</h2>
		</div>
		<hr>
		<div id = "task" class="alignHorizontal">
			<h1 class = "fraction">
				{numerator}
				<hr class="fraction-line">
				{denominator}
			</h1>	
			
			<h1>is equivalent to</h1>
			<h1>
				<input type="number" autocomplete="off" id = "answer" bind:value={input} on:keypress={ (e) => { if (e.charCode === 13) submitQuestion();} } />
			</h1>

			<h1>%</h1>
		</div>

		<br>
		<br>
		<br>

		{#if showExplanation}
			<div id = "explanation">
				<div class="alignHorizontal">
					<h2 class = "fraction">
						{numerator} <hr class="fraction-line"> {denominator}
					</h2>
					<h2>= {(numerator / denominator * 100).toFixed(2)}%</h2>
				</div>
				{#if numerator > 1}
					<div class="alignHorizontal">
						<h2>Because</h2>
						<h2 class = "fraction">
							{1} <hr class="fraction-line"> {denominator}
						</h2>
						<h2>= {(1/denominator*100).toFixed(2)}%</h2>
					</div>
					<div class="alignHorizontal">
						<h2>So, {numerator} • </h2>
						<h2 class = "fraction">
							{1} <hr class="fraction-line"> {denominator}
						</h2>
						<h2>={(numerator / denominator * 100).toFixed(2)}% </h2>
					</div>
				{/if}
			</div>
		{/if}
		
		<br>

		<div>
			<img src="images/explanationImage.png" on:click={() => {showExplanation = !showExplanation}}>
			<img src="images/confirmImage.png" on:click={submitQuestion}>
		</div>

		
	</div>
</div>