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

  @media (max-height: 800px) {
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
  {/if}
</main>
