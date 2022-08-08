<script>
	let players = [];
	let teams = ["Red", "Blue"];
	let teamSize = 2;

	let teamPlayers = [];

	function newName() {
		let fakePlayers = players;
		fakePlayers.push("");
        fakePlayers.push("");
		players = fakePlayers;
		console.table(players);
	}

	// create a random number between two numbers
	function randomIntFromInterval(min, max) {
		return Math.floor(Math.random() * (max - min + 1) + min);
	}

	// create random teams from the players array and the teams array with each team having the same number of players as teamSize, store in an array of objects
	function randomTeams() {
		let teamsArray = [];
		let playersArray = [...players];
		let teamsArrayLength = Math.ceil(playersArray.length / teamSize);
		for (let i = 0; i < teamsArrayLength; i++) {
			let team = {};
			team.name = teams[i];
			team.players = [];
			for (let j = 0; j < teamSize; j++) {
				let randomPlayerIndex = randomIntFromInterval(
					0,
					playersArray.length - 1
				);
				team.players.push(playersArray[randomPlayerIndex]);
				playersArray.splice(randomPlayerIndex, 1);
			}
			teamsArray.push(team);
		}
		return teamsArray;
	}

    function bgColour(colour) {
        if (colour == "Red") {
            return "bg-danger";
        } else if (colour == "Blue") {
            return "bg-primary";
        } else if (colour == "Green") {
            return "bg-success";
        } else if (colour == "Yellow") {
            return "bg-warning";
        } else if (colour == "Orange") {
            return "bg-orange";
        } else if (colour == "Purple") {
            return "bg-purple";
        } else if (colour == "Pink") {
            return "bg-pink";
        } else if (colour == "Brown") {
            return "bg-brown";
        } else if (colour == "Grey") {
            return "bg-grey";
        } else if (colour == "Black") {
            return "bg-black";
        } else if (colour == "White") {
            return "bg-white";
        } else {
            return "bg-secondary";
        }
    }

	console.log(randomTeams());
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
				{#each players as player}
					<tr>
						<td>
							<input bind:value={player} type="text" class="form-control" />
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
		<button on:click={newName} class="btn btn-primary"
			><strong>+</strong></button
		>
        <button class="btn btn-success" style="margin-top: 20px;" on:click={() => teamPlayers = randomTeams()}>Create Teams</button>
        <div class="card" style="width: 18rem; padding: 10px;">
            {#each teamPlayers as team}
                <div class="card {bgColour(team.name)}" style="padding: 10px;">
                    <h5>{team.name}</h5>
                    {#each team.players as player}
                        <samp>/team join {team.name} {player}</samp>
                        <br>
                    {/each}
                </div>
            {/each}
        </div>
	</div>
</main>
