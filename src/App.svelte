<script>
  import { writable } from "svelte/store";
  import { tweened } from "svelte/motion";
  import { cubicIn } from "svelte/easing";
  import { fade, fly, slide, scale } from "svelte/transition";

  import Spring from "./Spring.svelte";

  let boxInput;

  const progress = tweened(0, {
    delay: 0,
    duration: 400, // default = 400
    easing: cubicIn
  });

  setTimeout(() => {
    progress.set(0.5);
  }, 1500);

  let boxes = [];

  function addBox(value) {
    boxes = [...boxes, value];
  }

  // for (let i = 1; i <= 5; i++) {
  //     addBox(i.toString());
  // }

  let contrib = [];
  let i = 0;

  setInterval(() => {
    if (i < 30) {
      i++;
      addBox(i);
    }
  }, 300);
</script>

<style>
  div {
    width: 1rem;
    height: 1rem;
    background: #ccc;
    margin: 1rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    border-radius: 5px;
    padding: 1rem;
  }
  .year {
    height: 600px;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
  }
</style>

<!-- <progress value={$progress}></progress> -->
<!-- <Spring /> -->

<!-- <input type="text" bind:this={boxInput}>
<button on:click={addBox}>Add</button> -->

<section class="year">
  {#each boxes as box (box)}
    <div transition:scale={{ delay: 0, duration: 300 }}>{box}</div>
  {/each}
</section>
