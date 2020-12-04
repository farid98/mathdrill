<script>
    import { onMount } from "svelte";
    import { state } from "./store.js";
    import { tables } from "./store.js";


  
    var sum = "";
    var numOne = 1;
    var numTwo = 2;
  
    var showing = false;
  
    onMount(async () => {
      await showAnother();
      console.log("in Practice-show another")
    });


function showHome() {
    state.update(() => 0); 
}

  
    function showAnother() {


      console.log("gonna pick numone")

      do  {
        numOne = Math.floor(Math.random() * 9 + 2);
        console.log (numOne)
      } while ($tables[numOne - 2] == 0)
      
      numTwo = Math.floor(Math.random() * 9 + 2);
      sum = numOne + " x " + numTwo;
      showing = false;
    }
  
    function showMe() {
      showing = true;
    }
  </script>
  
  <section class="hero is-link">
    <div class="hero-body">
      <div class="container">
  
          <div class="columns is-mobile">
              <div class="column is-10 is-size-3">
                  Practice Time !
              </div>
              <div class="column is narrow is-size-3">
                  <span on:click="{showHome}"  class="icon">
                      <i class="fas fa-home"></i>
                    </span>
              </div>
          </div>
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

<!-- <div class="section">

  <div class="buttons is-centered">
    <button on:click={showHome} class="button is-info is-large">End Practice
      </button>
   </div>

</div> -->