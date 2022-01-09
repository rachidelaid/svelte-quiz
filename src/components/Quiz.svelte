<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  import { fly } from 'svelte/transition';
  export let question;

  let answer = '';

  $: answers = [...question.incorrect_answers, question.correct_answer].sort(
    () => Math.random() - 0.5
  );

  let borderElm;

  const choose = (e) => {
    answer = e.target.id;
    borderElm.style.visibility = 'visible';
    borderElm.style.width = 0;
    setTimeout(() => {
      dispatch('choose', answer);
      borderElm.style.visibility = 'hidden';
      borderElm.style.width = '100%';
      answer = '';
    }, 2000);
  };
</script>

<section class="quiz">
  <div
    class="card"
    in:fly={{ x: 200, duration: 200 }}
    out:fly={{ x: -200, duration: 200 }}
  >
    <h2>{@html question.question}</h2>
    {#each answers as ans (ans)}
      <div class="btn" id={ans} on:click|once={choose}>{@html ans}</div>
    {/each}

    <hr id="border" bind:this={borderElm} />
    {#if answer !== '' && answer === question.correct_answer}
      <p>Correct!</p>
    {/if}

    {#if answer !== '' && answer !== question.correct_answer}
      <p>Incorrect!</p>
    {/if}
  </div>
</section>

<style>
  .quiz {
    margin: 50px;
  }

  hr {
    border: none;
    background-color: #d3d3d3;
    height: 2px;
    margin: 20px 0 0 0;
    width: 100%;
    transition: width 2s ease-in-out;
    visibility: hidden;
  }

  p {
    margin: 0;
  }
</style>
