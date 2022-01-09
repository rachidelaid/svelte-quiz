<script>
  import { fly } from 'svelte/transition';
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let score = 0;
  export let seconds = 0;

  let userName = '';

  const save = () => {
    dispatch('save', userName);
  };
</script>

<section class="result">
  <div
    class="card"
    in:fly={{ x: 200, duration: 200 }}
    out:fly={{ x: -200, duration: 200 }}
  >
    <h2>All done!</h2>
    <p>You managed to score {score} in {seconds} seconds.</p>

    <div class="form">
      <label for="userName">
        Enter your name:
        <input
          type="text"
          id="userName"
          name="userName"
          bind:value={userName}
        />
      </label>
      <button on:click={save}>Submit</button>
    </div>
  </div>
</section>

<style>
  .result {
    margin: 50px auto;
    width: fit-content;
  }
</style>
