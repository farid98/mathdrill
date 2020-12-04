<script>
  import { onMount } from "svelte";
  import { children } from "svelte/internal";
  import { state } from "./store.js";
  import { tables } from "./store.js";


  var sum = "x";
  var numOne = 1;
  var numTwo = 2;
  var choice = [0, 1, 2];
  var totalQuestions = 10;
  var currentQuestion = 0;
  var correctAnswers = 0;
  var answered = false;
  var answerIsCorrect = false;
  var quizOver = false;

  onMount(async () => {
    await showAnother();
  });

  function answerGiven(ans) {
    if (answered) return;
    answered = true;

    if (numOne * numTwo == choice[ans]) {
      answerIsCorrect = true;
    } else {
      answerIsCorrect = false;
    }

    if (answerIsCorrect) correctAnswers++;
  }

  function showHome() {
    state.update(() => 0);
  }

  function showAnother() {
    currentQuestion += 1;

    if (currentQuestion > totalQuestions) {
      quizOver = true;
    }

    answered = false;
    console.log("in Quiz-show another");

    do  {
        numOne = Math.floor(Math.random() * 9 + 2);
      } while ($tables[numOne - 2] == 0)

    numTwo = Math.floor(Math.random() * 9 + 2);
    sum = numOne + " x " + numTwo;

    var correctNum = Math.floor(Math.random() * 3);

    console.log("choice generation");
    choice[correctNum] = numOne * numTwo;
    console.log(choice);

    for (var x = 0; x < 3; x++) {
      console.log(x);
      if (x == correctNum) continue;
      console.log("changing");

      var tt = 0;
      var pp = 0;
      do {
        if (Math.floor(Math.random() == 0)) {
          tt = numOne;
        } else tt = numTwo;
        pp = tt * Math.floor(Math.random() * 9 + 1);
      } while (choice.includes(pp));
      choice[x] = pp;
    }
  }
</script>

<section class="hero is-link">
  <div class="hero-body">
    <div class="container">
      <div class="columns is-mobile">
        <div class="column is-10 is-size-3">Quiz Time !</div>
        <div class="column is narrow is-size-3">
          <span on:click={showHome} class="icon ">
            <i class="fas fa-home" />
          </span>
        </div>
      </div>
    </div>
  </div>
</section>

{#if quizOver}
  <div class="section">
    <div class="columns is-centered">
      <div class="column is-6">
        <div class="notification is-primary is-size-1 has-text-centered">
          <p>Quiz Over</p>
          <p>You got {correctAnswers} out of {totalQuestions}</p>

          <button
            on:click={showHome}
            class="button is-danger is-medium mt-4">Home
          </button>
        </div>
      </div>
    </div>
  </div>
{:else}
  <!-- Quiz in progress, show the question and options -->
  <div class="section">
    <div class="columns is-centered">
      <div class="column is-6">
        <h1 class="has-text-centered">{currentQuestion} of {totalQuestions}</h1>
        <div class="notification is-primary is-size-1 has-text-centered">
          {sum}
        </div>
      </div>
    </div>
  </div>

  <div class="columns is-centered">
    <div class="column is-6">
      <div class="columns is-centered is-mobile">
        {#each Array(3) as _, row}
          <div class="column  has-text-centered">
            <div class="box" on:click={() => answerGiven(row)}>
              {choice[row]}
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>

  {#if answered}
    <!-- Show the next button and tell if answer was right or wrong -->
    <section>
      <div class="columns is-centered">
        <div class="column is-6 is-centered has-text-centered">
          <div class="notification">
            {#if answerIsCorrect}
              <h1>Correct !</h1>
            {:else}
              <h1>Sorry. {sum} makes {numOne * numTwo}</h1>
            {/if}
          </div>
          <div class="buttons is-centered">
            <button
              on:click={showAnother}
              class="button is-primary is-large">Next</button>
          </div>
        </div>
      </div>
    </section>
  {/if}
{/if}

<!-- <div class="section">
  <div class="buttons is-centered">
    <button on:click={showHome} class="button is-link is-large">End Quiz
    </button>
  </div>
</div> -->
