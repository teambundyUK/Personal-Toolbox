<script>
	import StableAnimation from "./StableAnimation.svelte";
	import GunRandomTeams from "./GunRandomTeams.svelte";
	import PromptBuilder from "./PromptBuilder.svelte";
</script>

<svelte:head>
	<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Rounded:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" />
</svelte:head>

<main>
	<div class="container">
		<div class="row">
			<div class="col">
				<div class="tool">
					<StableAnimation />
				</div>
			</div>
			<div class="col">
				<div class="tool">
					<GunRandomTeams />
				</div>
			</div>
			<div class="col">
				<div class="tool">
					<PromptBuilder />
				</div>
			</div>
		</div>
	</div>
</main>

<style>
</style>
