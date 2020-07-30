<script>
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";
  import { quintOut } from "svelte/easing";

  import snarkdown from "snarkdown";
  import Card from "./Card.svelte";

  let taco = {};
  let loading = false;
  let sectionCount;
  let currentStep = 0;
  let ready = true;
  $: direction = "right"; //right

  async function getRandomRecipe() {
    loading = true;
    const res = await fetch("http://taco-randomizer.herokuapp.com/random/");
    const tacoResult = await res.json();
    parseTaco(tacoResult);
  }

  function parseTaco(tacoResult) {
    Object.keys(tacoResult).map((tk) => {
      const recipe = tacoResult[tk].recipe.replace(
        new RegExp(/(tags)(.*)/, "g"),
        ""
      );
      console.log(recipe);
      taco[tk] = snarkdown(recipe);
    });
    sectionCount = Object.keys(tacoResult).length - 1;
    loading = false;
  }

  async function moveStep(nextStep) {
    direction = nextStep > currentStep ? "right" : "left";
    currentStep = nextStep;
    ready = false;
    await sleep(200);
    ready = true;
  }

  function sleep(time) {
    return new Promise((fulfill) => {
      setTimeout(fulfill, time);
    });
  }

  onMount(() => {
    getRandomRecipe();
  });
</script>

<style>
  main {
    margin: 20px;
  }

  .left,
  .right {
    position: absolute;
    top: 50%;
  }
  .left {
    left: 1em;
  }
  .right {
    right: 1em;
  }
</style>

<main>
  {#if !loading}
    {#if currentStep > 0}
      <button class="left" on:click={() => moveStep(currentStep - 1)}>
        left
      </button>
    {/if}

    {#each Object.keys(taco) as layer, i}
      {#if ready && currentStep == i}
        <div
          in:fly={{ duration: 200, x: direction == 'right' ? 200 : -200, easing: quintOut }}
          out:fly={{ duration: 200, x: direction == 'right' ? -200 : 200, easing: quintOut }}>
          <Card tacoLayer={taco[layer]} name={layer} />
        </div>
      {/if}
    {/each}

    {#if currentStep < sectionCount}
      <button class="right" on:click={() => moveStep(currentStep + 1)}>
        Right
      </button>
    {/if}
  {:else}loading{/if}
</main>
