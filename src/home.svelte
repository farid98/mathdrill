<script>
import { toggle_class } from "svelte/internal";

import { state } from "./store.js";
import { tables } from "./store.js";

  function showQuiz() {
    if (!$tables.includes(1)) return // dont go until at least something is picked
    state.update(() => 2);
  }

  function showPractice() {
    if (!$tables.includes(1)) return // dont go until at least something is picked

    state.update(() => 1);
  }

  function toggle(i) {

    if ($tables[i] == 1 )
        $tables[i]  = 0; 
        else
        $tables[i]  = 1; 

    }


</script>

<section class="hero is-link">
  <div class="hero-body">
    <div class="container">
      <h1 class="title">Hi :)</h1>
      <h1 class="subtitle">Let's learn the times tables</h1>
    </div>
  </div>
</section>

<div class="section">
  <button on:click={showQuiz} class="button is-primary is-large">Take a Quiz
  </button>
  <p />
  <button on:click={showPractice} class="button is-danger is-large">or Practice
    &nbsp;
  </button>
</div>



<div class="title ">Choose tables to practice:</div>


{#each $tables as t, row}

    {#if t == 1}
    <p  on:click={ () => toggle(row)   } class="button ml-2 is-link ">{row + 2}</p>
    
    {:else}
    <p on:click={ () => toggle(row)   } class="button ml-2 is-light ">{row + 2}</p>
    {/if}



{/each}



{#if (!$tables.includes(1))}

  <div class="title mt-4  has-text-danger ">Please choose at least one</div>

{/if}

