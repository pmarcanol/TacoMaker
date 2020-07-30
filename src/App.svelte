<script>
  import Recipe from "./Recipe.svelte";

  const screens = {
    home: "home",
    recipe: "recipe",
  };
  let screen = screens.recipe;
  let getNewRecipe = false;
</script>

<style>
  :global(body) {
    padding: 0;
    overflow: hidden;
  }
  :global(body::after) {
    content: "";
    position: absolute;
    width: 200%;
    height: 200%;
    top: -50%;
    left: -50%;
    z-index: -1;
    background-image: url("/imgs/taco.svg");
    background-size: 124px;
    background-position: 20 20;
    background-repeat: space;
    background-color: rgb(255, 247, 173);
    transform: rotate(-45deg);
  }
  main {
    min-height: 100%;
    min-width: 100%;
    padding: 0;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  h1 {
    margin: 0;
    color: rgb(70, 28, 28);
    text-transform: uppercase;
    font-weight: 300;
    margin: 1em;
    font-size: 50px;
    text-align: center;
  }

  button {
    background: crimson;
    color: white;
    border-radius: 10px;
    border: none;
    padding: 1em 2em;
    text-transform: uppercase;
    transition: padding 150ms ease-in-out, font-size 100ms ease;
  }

  button:hover {
    font-size: 1.2em;
  }
  button:hover:active {
    font-size: 1.17em;
    background-color: crimson;
  }
</style>

<main>
  {#if screen == screens.home}
    <h1>Taco Maker</h1>
    <button on:click={() => (screen = screens.recipe)}>Get My Taco!</button>
  {:else if screen == screens.recipe && !getNewRecipe}
    <Recipe />
    <button
      on:click={() => {
        getNewRecipe = true;
        getNewRecipe = false;
      }}>
      Get New Recipe
    </button>
  {/if}
</main>
