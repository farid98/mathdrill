<script>
  import Practice from "./practice.svelte";
  import Quiz from "./quiz.svelte";
  import Home from "./home.svelte";
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
	<Home />	

	
  {/if}
</div>

