<script>
    let prompt = ["Trending","Artstation"]
</script>

<main>
    <div style="height: 100vh; width: 150px; text-aligin: centered;">
		<h5><strong>Random Team Commands</strong></h5>
		<table class="table">
			<thead>
				<tr>
					<th scope="col">Username:</th>
				</tr>
			</thead>
			<tbody>
				{#each prompt as chunk}
					<tr>
						<td>
							<input bind:value={chunk} type="text" class="form-control" />
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
		
    </div>
</main>

<style>

</style>