<script>
  import { fly } from 'svelte/transition';

  const scores = localStorage.getItem('board')
    ? JSON.parse(localStorage.getItem('board'))
    : [];
</script>

<section
  class="card"
  in:fly={{ x: 200, duration: 200 }}
  out:fly={{ x: -200, duration: 200 }}
>
  {#if scores.length === 0}
    <p>No Scores</p>
  {:else}
    <h3>Score Board</h3>
    {#each scores as score (score.name)}
      <p><b>{score.name}:</b> {score.score}</p>
    {/each}
  {/if}
</section>

<style>
  .card {
    margin: 50px;
  }
</style>
