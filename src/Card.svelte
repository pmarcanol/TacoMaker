<script>
  import { getNameFromObjectKey } from "./utils";

  export let tacoLayer;
  export let name;
</script>

<style>
  .card {
    background: rgb(72, 110, 84);
    padding: 1em;
    border-radius: 10px;
    max-width: 70%;
    max-height: 70%;
    overflow-y: auto;
    border: 3px solid #f1855b;
    margin: auto;
    color: white;
    box-sizing: border-box;
    margin-block-end: 2em;
  }

  @media (max-width: 640px) {
    .card {
      max-width: 100%;
      width: 100%;
      max-height: 80vh;
      padding-top: 0;
    }
  }

  h1 {
    text-transform: capitalize;
    color: #ffda4c;
    width: 100%;
    display: flex;
    justify-content: center;
    margin: 0;
    text-shadow: -2px 2px #fd5858;
  }
  p {
    padding-bottom: 2em;
  }
</style>

<div class="card">
  <h1 class="title">{getNameFromObjectKey(name)}</h1>
  <p>
    {@html tacoLayer}
  </p>
</div>
