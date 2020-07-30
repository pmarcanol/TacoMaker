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

  main {
    height: 100%;
    width: 100%;
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

  .new-recipe {
    position: absolute;
    bottom: 2em;
  }

  @media (max-height: 640px) {
    .new-recipe {
      bottom: 0;
    }
    main {
      justify-content: flex-start;
    }
  }
</style>

<main>
  {#if screen == screens.home}
    <h1>Taco Maker</h1>
    <button on:click={() => (screen = screens.recipe)}>Get My Taco!</button>
  {:else if screen == screens.recipe && !getNewRecipe}
    <Recipe />
    <button
      class="new-recipe"
      on:click={() => {
        getNewRecipe = true;
        getNewRecipe = false;
      }}>
      Get New Recipe
    </button>
  {/if}
</main>
