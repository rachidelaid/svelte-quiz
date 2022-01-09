<script>
  import { fly } from 'svelte/transition';
</script>

<section
  in:fly={{ x: 200, duration: 200 }}
  out:fly={{ x: -200, duration: 200 }}
  class="card loading"
>
  <img src="loading.gif" alt="loading" />
</section>
