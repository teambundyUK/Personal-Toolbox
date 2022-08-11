<script>
	import AutoComplete from "simple-svelte-autocomplete"

	const chunks = ["light", "peaceful", "calm", "serene", "soothing", "relaxed", "placid", "comforting", "cosy", "tranquil", "quiet", "pastel", "delicate", "graceful", "subtle", "balmy", "mild", "ethereal", "elegant", "tender", "soft", "light", "bright", "vibrant", "dynamic", "spirited", "vivid", "lively", "energetic", "colorful", "joyful", "romantic", "expressive", "bright", "rich", "kaleidoscopic", "psychedelic", "saturated", "ecstatic", "brash", "exciting", "passionate", "hot"]

    let prompt = []
	let selectedChunk
	let meta = "!dream "

	let builtPrompt = ""

	function addChunk() {
		let tempPrompt = prompt
		tempPrompt.push(selectedChunk)
		prompt = tempPrompt
		selectedChunk = ""
	}

	function removeChunk(index) {
		let tempPrompt = prompt
		tempPrompt.splice(index, 1)
		prompt = tempPrompt
	}

	function moveChunkUp(index) {
		let tempPrompt = prompt
		let tempChunk = tempPrompt[index]
		tempPrompt[index] = tempPrompt[index - 1]
		tempPrompt[index - 1] = tempChunk
		prompt = tempPrompt
	}

	function moveChunkDown(index) {
		let tempPrompt = prompt
		let tempChunk = tempPrompt[index]
		tempPrompt[index] = tempPrompt[index + 1]
		tempPrompt[index + 1] = tempChunk
		prompt = tempPrompt
	}

	function buildPrompt() {
		let allChunks = "";
		// iterate over every item in the chunks array
		for (let i = 0; i < prompt.length; i++) {
			let chunk = prompt[i];
			allChunks = allChunks + chunk + " ";
		}
		builtPrompt = meta + allChunks + "-n 9 -g -C 8"
	}

	function copyPrompt() {
		navigator.clipboard.writeText(builtPrompt)
	}

	function clearPrompt() {
		prompt = []
		builtPrompt = ""
	}

	function duplicateChunk(index) {
		let tempPrompt = prompt
		tempPrompt.splice(index, 0, tempPrompt[index])
		prompt = tempPrompt
	}
</script>

<main>
    <div style="height: 100vh; width: 150px; text-aligin: centered;">
		<h5><strong>Prompt Builder</strong></h5>
		<table class="table">
			<thead>
				<tr>
					<th scope="col">Control:</th>
					<th scope="col">Chunks:</th>
					<th class="col">Remove:</th>
				</tr>
			</thead>
			<tbody>
				{#each prompt as chunk, index}
					<tr>
						<td>
							<button class="btn btn-success" on:click={() => moveChunkUp(index)}>
								<span class="material-symbols-rounded">
									expand_less
								</span>
							</button>
							<button class="btn btn-success" style="margin-top: 10px;" on:click={() => moveChunkDown(index)}>
								<span class="material-symbols-rounded">
									expand_more
								</span>
							</button>
						</td>
						<td>
							<input bind:value={chunk} type="text" class="form-control" style="margin-top: 25px; width: 100px;"/>
						</td>
						<td>
							<button class="btn btn-danger" style="margin-top: 10px;" on:click={() => removeChunk(index)}>
								<span class="material-symbols-rounded">
									close
								</span>
							</button>
							<button class="btn btn-primary" style="margin-top: 10px;" on:click={() => duplicateChunk(index)}>
								<span class="material-symbols-rounded">
									content_copy
								</span>
							</button>
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
		<AutoComplete items={chunks} bind:selectedItem={selectedChunk} hideArrow={true}/><button on:click={addChunk} class="btn btn-primary"
		><strong><span class="material-symbols-rounded">
			add
			</span></strong></button><button on:click={clearPrompt} class="btn btn-danger"
		><strong><span class="material-symbols-rounded">
			delete_forever
			</span></strong></button>
		<button class="btn btn-warning" style="margin-top: 10px;" on:click={buildPrompt}>
			<span class="material-symbols-rounded">
				print
				</span>
		</button>
		<input bind:value={builtPrompt} type="text" class="form-control" style="margin-top: 10px;"/><button on:click={copyPrompt} class="btn btn-primary"><span class="material-symbols-rounded">
			content_copy
		</span></button>
    </div>
</main>

<style>

</style>