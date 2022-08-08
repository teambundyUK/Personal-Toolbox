<script>
	import { createEventDispatcher } from "svelte";

	export let prompt;
	export let number;
	export let progress;
	export let disabled;
	export let progressFinished;

	const dispatch = createEventDispatcher();

	function copy() {
		navigator.clipboard.writeText(prompt);
		dispatch("next");
	}
</script>

<main>
	<div style="margin: 10px;">
		<p>{prompt}</p>
		<br />
		<h5><strong>Number: </strong>{number}</h5>
		<br />
		<button {disabled} class="btn btn-primary" on:click={copy}>Copy</button>
		<br />
		<div class="progress" style="margin-top: 20px;">
			<div
				class="progress-bar progress-bar-striped progress-bar-animated {progressFinished}"
				role="progressbar"
				style="width: {progress}%;"
			/>
		</div>
	</div>
</main>
