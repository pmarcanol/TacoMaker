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
    max-width: 70vw;
    max-height: 70vh;
    overflow-y: auto;
    border: 3px solid #f1855b;
    margin: auto;
    color: white;
    box-sizing: border-box;
    margin-block-end: 2em;
  }

  @media (max-width: 640px) {
    .card {
      max-width: 100vw;
      width: 100vw;
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
    text-transform: uppercase;
  }
  p {
    padding-bottom: 2em;
    font-weight: 100;
  }

  :global(.card p h1),
  :global(.card p h2) {
    text-align: center;
    font-weight: bolder;
    color: #ffda4c;
    text-transform: capitalize;
  }
  :global(.card li:before) {
    content: "🥑";
    margin-left: -21px;
    margin-right: 10px;
  }

  :global(.card a) {
    color: rgb(255, 239, 0);
  }
</style>

<div class="card">
  <h1 class="title">{getNameFromObjectKey(name)}</h1>
  <p>
    {@html tacoLayer}
  </p>

</div>
