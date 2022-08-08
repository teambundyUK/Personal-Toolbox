<script>
	import Copy from "./Copy.svelte";

	let seed = 3980591359;
	let inputPrompt = "A %$% year old tree, fantasy painting, lots of detail";
	let steps = 100;
	let number = 1;
	let prompt;
	let totalFrames = 10;
	let finished = false;
	let disabled;
	let progressFinished;

	buildPrompt();

	$: progress = Math.round((number / totalFrames) * 100);

	function increment() {
		if (number < totalFrames) {
			number += 1;
			buildPrompt();
		} else {
			finished = true;
			disabled = "disabled";
			progressFinished = "bg-success";
		}
	}

	function buildPrompt() {
		prompt = inputPrompt.replace("%$%", number);
		prompt = `!dream ${prompt} -s ${steps} -S ${seed}`;
	}
</script>

<main>
	<div style="height: 100vh; width: 150px; text-aligin: centered;">
		<h5><strong>Animation Tool</strong></h5>
		<label for="prompt">Prompt:</label>
		<input
			type="text"
			class="form-control"
			placeholder="Input prompt..."
			bind:value={inputPrompt}
			style="width: 290px; margin-bottom: 10px;"
			id="prompt"
		/>
		<label for="seed">Seed:</label>
		<input
			type="number"
			class="form-control"
			bind:value={seed}
			style="width: 290px; margin-bottom: 10px;"
			id="seed"
		/>
		<label for="steps">Steps: {steps}</label>
		<input
			type="range"
			max="150"
			min="1"
			bind:value={steps}
			class="form-range"
			style="width: 290px;"
			id="steps"
		/>
		<div class="card" style="width: 18rem;">
			<Copy
				{prompt}
				{number}
				on:next={increment}
				{progress}
				{disabled}
				{progressFinished}
			/>
		</div>
	</div>
</main>
