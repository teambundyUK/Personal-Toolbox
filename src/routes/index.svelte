<script>
	import StableAnimation from "./StableAnimation.svelte";
	import GunRandomTeams from "./GunRandomTeams.svelte";
	import PromptBuilder from "./PromptBuilder.svelte";
</script>

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
