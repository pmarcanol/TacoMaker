<script>
  import Recipe from "./Recipe.svelte";

  const screens = {
    home: "home",
    recipe: "recipe",
  };
  let screen = screens.home;
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
    font-weight: bold;
    font-size: 50px;
    margin: 0;
    margin-bottom: 1em;
    text-transform: capitalize;
    text-align: center;
    color: #ba0000;
    display: flex;
    background-color: #fff7ad;
    justify-content: center;
    text-transform: uppercase;
  }
  @media (max-height: 800px) {
    main {
      justify-content: flex-start;
    }
  }
</style>

<main>
  {#if screen == screens.home}
    <h1>Taco Randomizer</h1>
    <button on:click={() => (screen = screens.recipe)}>Get My Taco!</button>
  {:else if screen == screens.recipe && !getNewRecipe}
    <Recipe />
  {/if}
</main>
