<script>
    import { setContext } from "svelte/internal";
    import Card from "./Card.svelte";
    import Login from "./Login.svelte";

    function handleVoting() {
    	// do nothing (meme)
  	}

	let teams = [];

	let ch1 = 0;
	let ch2 = 0;
	let ch3 = 0;

	let medal = 3;

	function setMedal(id) {
		const pre_medal = medal;
		switch (medal) {
			case 3:
				ch1 = id;
				console.log('🤓');
				medal = 2;
				break;
			case 2:
				ch2 = id;
				console.log('👆');
				medal = 1;
				break;
			case 1:
				ch3 = id;
				console.log('😎👈');
				medal = null;
			default:
				break;
		}

		return pre_medal;
	}

	setContext('setMedal', setMedal);

	fetch("/src/assets/teams.json", {method: 'GET', headers: {'Content-Type': 'application/json'}})
	.then(res => {
		res.json()
		.then(json => {
			teams = json;
			console.log(teams);
		});
	});
</script>

<div class="voting">
    <div class="voting__header">
    <h2>Kto zajmie 1. miejsce?</h2>
    </div>

	<div id="team_view">
		{#each teams as team}
			<Card country_id={team.id} country_name="{team.name}" flag_image="{team.img}"/>
		{/each}
	</div>

    <div class="voting__submit">
        <button on:click={handleVoting}>
            Oddaj głos
        </button>
    </div>
</div>

<Login bind:firstChoice={ch1} bind:secondChoice={ch2} bind:thirdChoice={ch3} />

<style>
	#team_view {
		width: 100%;
		overflow-y: scroll;
		overflow-x: hidden;
		height: 70vh;
		display: grid;
		flex-direction: column;
		grid-template-columns: repeat(2, 1fr);
		gap: calc(2vw - .2rem);
		width: 100%;
		padding: 1rem;
  		grid-column-start: span 2;
		flex-wrap: wrap;
	}
</style>