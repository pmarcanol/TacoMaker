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
  let direction = "right"; //right

  async function getRandomRecipe() {
    loading = true;
    const res = await fetch("http://taco-randomizer.herokuapp.com/random/");
    const tacoResult = await res.json();
    parseTaco(tacoResult);
  }

  async function getRecipe() {
    ready = false;
    taco = {};
    await getRandomRecipe();
    currentStep = 0;
    loading = false;
    await sleep(200);
    ready = true;
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
  .left,
  .right {
    position: absolute;
    top: 50%;
    border-radius: 50%;
    width: 3em;
    height: 3em;
    font-size: unset;
    padding: 0;
  }
  .left span,
  .right span {
    width: 100%;
    height: 100%;
    margin-top: -5px;
    margin-left: -2px;
    justify-content: center;
    align-items: center;
    display: flex;
  }

  .right span {
    margin-left: 2px;
  }
  .left:active,
  .right:active {
    font-size: 0.97em;
  }
  .left {
    left: 1em;
  }
  .right {
    right: 1em;
  }

  .new-recipe {
    position: absolute;
    bottom: 2em;
    left: 50%;
    transform: translateX(-50%);
  }
  
  .loading {
    font-size: 60px;
    animation: spin 1s linear infinite;
    position: absolute;
    left: 50%;
  }

  @keyframes spin {
    100% {
      transform: rotate(360deg);
    }
  }

  @media (max-height: 940px) {
    .new-recipe {
      bottom: 0;
    }

    .left,
    .right {
      top: auto;
      bottom: 3em;
    }
  }
</style>

<div>
  {#if !loading}
    {#if currentStep > 0}
      <button class="left" on:click={() => moveStep(currentStep - 1)}>
        <span>👈</span>
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
        <span>👉</span>
      </button>
    {/if}
  {:else}
    <div class="loading">🌶️</div>
  {/if}
  <button class="new-recipe" on:click={getRecipe}>Get New Recipe</button>
</div>
