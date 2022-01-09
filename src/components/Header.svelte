<script>
  export let seconds = 0;
</script>

<nav>
  <div class="highScore" on:click>View highscores</div>

  <p>Time: <b>{seconds}</b></p>
</nav>

<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background-color: #23837f;
    color: #fff;
  }

  .highScore {
    cursor: pointer;
  }

  .highScore:hover {
    font-weight: bold;
  }
</style>
