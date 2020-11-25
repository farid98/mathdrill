<script>
  import Practice from "./practice.svelte";
  import Quiz from "./quiz.svelte";
  import { state } from "./store.js";


//  var state = 2; // 0 = home screen. 1 = Quiz. 2 = practice

function showQuiz() {
	state.update(() => 2);
}

function showPractice() {
	state.update(() => 1);}

</script>



<div class="container">
  {#if $state == 1}
    <Practice />
  {:else if $state == 2} 
	<Quiz />
	{:else}
	
	<section class="hero is-link">
		<div class="hero-body">
		  <div class="container">
			<h1 class="title">Hi :) </h1>
			<h1 class="subtitle">Let's learn the times tables</h1>
		  </div>
		</div>
	  </section>
	  
	<div class="section">

			<button on:click={showQuiz} class="button is-primary is-large">Take a Quiz
			  </button>
			  <p></p>
			<button on:click={showPractice} class="button is-danger is-large">or Practice &nbsp;  </button>
	
	</div>
	
  {/if}
</div>

