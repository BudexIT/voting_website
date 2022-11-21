<script>
    import { setContext } from "svelte";
    import Info from "./Info.svelte";

  import Login from "./Login.svelte";
  import Vote from "./Vote.svelte";

  let votedAlready = false;

  setContext("voteSuccessful", () => {
	votedAlready = true;
  });

</script>

<main>
  <div class="wrapper">
    <div class="section--left">
    </div>
    <div class="section--right">
		{#if !votedAlready}
			<Vote />
		{:else}
			<Info />
		{/if}
    </div>
  </div>
</main>