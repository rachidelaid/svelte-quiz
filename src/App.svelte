<script>
  import Header from './components/Header.svelte';
  import Start from './components/Start.svelte';
  import Quiz from './components/Quiz.svelte';
  import Result from './components/Result.svelte';
  import Loading from './components/Loading.svelte';
  import Board from './components/Board.svelte';

  import { onDestroy } from 'svelte';

  let seconds = 0;
  let interval;

  const startTimer = () => {
    interval = setInterval(() => {
      seconds = seconds + 1;
    }, 1000);
  };

  onDestroy(() => clearInterval(interval));

  let arr;
  let index = 0;
  let score = 0;

  let state = 'start';

  const startQuiz = async () => {
    state = 'quiz';

    const resp = await fetch(
      'https://opentdb.com/api.php?amount=10&category=18&type=multiple'
    );

    const data = await resp.json();

    arr = data.results;

    startTimer();
  };

  const answered = ({ detail: answer }) => {
    if (answer === arr[index].correct_answer) {
      score++;
    }
    index++;

    if (index === arr.length) {
      state = 'done';
      clearInterval(interval);
    }
  };

  const saveScore = ({ detail: userName }) => {
    console.log(userName);
    const arr = localStorage.getItem('board')
      ? JSON.parse(localStorage.getItem('board'))
      : [];

    const curScore = arr.find((s) => s.name === userName);
    if (!curScore) {
      arr.push({
        name: userName,
        score,
      });
    } else {
      if (score > curScore.score) {
        curScore.score = score;
      }
    }

    localStorage.setItem('board', JSON.stringify(arr));

    state = 'start';
    seconds = 0;
  };

  const toggleBoard = () => {
    if (state !== 'board') {
      state = 'board';
    } else {
      state = 'start';
    }
  };
</script>

<main>
  <Header on:click={toggleBoard} {seconds} />

  {#if state === 'board'}
    <Board />
  {/if}

  {#if state === 'start'}
    <Start on:click={startQuiz} />
  {/if}

  {#if state !== 'board' && state !== 'start' && !arr}
    <Loading />
  {/if}

  {#if arr && index < arr.length}
    <Quiz question={arr[index]} on:choose={answered} />
  {/if}

  {#if state === 'done'}
    <Result {score} {seconds} on:save={saveScore} />
  {/if}
</main>

<style>
</style>
