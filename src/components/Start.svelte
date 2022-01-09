<script>
  import { fly } from 'svelte/transition';
</script>

<section class="start">
  <div
    class="card"
    in:fly={{ x: 200, duration: 200 }}
    out:fly={{ x: -200, duration: 200 }}
  >
    <h2>Coding Quiz Challenge</h2>
    <p>
      Try to answer to following code-related questions withing the time limit.
    </p>
    <p>
      Keep in mind that incorrect answers will penalize your score/time by ten
      seconds!
    </p>
    <button on:click>Start</button>
  </div>
</section>

<style>
  .start {
    margin: 50px;
  }
</style>
