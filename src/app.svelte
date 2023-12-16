<script>
  import Game from './game.svelte';
  import { currentGame } from './stores';

  const play = ai => () => currentGame.start(ai);
</script>

<style>
</style>

<header>
  <div class="navbar navbar-dark bg-dark shadow-sm">
    <div class="container d-flex justify-content-between">
      <a href="/" class="navbar-brand d-flex align-items-center">
        <strong>WOPR.SAD</strong>
      </a>
    </div>
  </div>
</header>

<main>
  {#if !$currentGame}
    <section class="jumbotron text-center">
      <div class="container">
        <h1>Start playing now</h1>
        <p class='mt-3'>
          <button type='button' class="btn btn-success btn-lg" on:click={play('random')}>Easy mode</button>
          <button type='button' class="btn btn-danger btn-lg" on:click={play('wopr')}>Play against the WOPR</button>
        </p>
        <img src="https://www.reddit.com/media?url=https%3A%2F%2Fi.redd.it%2Fpfgnwoakg73c1.jpg">
      </div>
    </section>
  {/if}

  {#if $currentGame}
    <Game />
  {/if}

  {#if $currentGame && $currentGame.state !== 'playing'}
    <section class="text-center mt-4">
      <p>
        <button type='button' class="btn btn-success btn" on:click={play('random')}>Play again in easy mode</button>
        <button type='button' class="btn btn-danger btn" on:click={play('wopr')}>Play again against the WOPR</button>
      </p>
    </section>
  {/if}
</main>