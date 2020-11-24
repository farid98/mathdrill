<script>
  import { onMount } from "svelte";

  var sum = "";
  var numOne = 1;
  var numTwo = 2;

  var showing = false;

  onMount(async () => {
    await showAnother();
  });

  function showAnother() {
    numOne = Math.floor(Math.random() * 9 + 2);
    numTwo = Math.floor(Math.random() * 9 + 2);
    sum = numOne + " x " + numTwo;
    showing = false;
  }

  function showMe() {
    showing = true;
  }
</script>

<section class="hero is-primary">
  <div class="hero-body">
    <div class="container">
      <h1 class="title">Hi :)</h1>
      <h1 class="subtitle">Let's practice times tables</h1>
    </div>
  </div>
</section>

<div class="section">
  <div class="columns is-centered">
    <div class="column is-4">
      <div class="notification is-primary is-size-1">{sum}</div>

      <div class="notification is-danger is-size-1">
        <p>
          {#if showing}Makes: {numOne * numTwo}{:else}?{/if}
        </p>
      </div>
    </div>
  </div>
</div>
<section>
  <div class="columns is-centered">
    <div class="column is-4 is-centered has-text-centered">
      <div class="buttons is-centered">
        <button on:click={showAnother} class="button is-primary is-large">Try
          Another</button>
        <button on:click={showMe} class="button is-danger is-large">Show Me</button>
      </div>
    </div>
  </div>
</section>
