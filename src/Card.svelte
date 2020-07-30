<script>
  import { getNameFromObjectKey } from "./utils";

  export let tacoLayer;
  export let name;
</script>

<style>
  .card {
    background: rgb(255, 255, 255);
    padding: 2em;
    border-radius: 10px;
    max-width: 70%;
    max-height: 70%;

    margin: auto;
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
</style>

<div class="card">
  <h1 class="title">{getNameFromObjectKey(name)}</h1>
  {@html tacoLayer}
</div>
