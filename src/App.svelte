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
    if (i < 336) {
      i++;
      addBox(i);
    }
  }, 1);
</script>

<style>
  div {
    font-size: 0.1rem;
    width: .45rem;
    height: .45rem;
    margin: 0.1rem;
    padding: 0.1rem;
  }
  .year {
      margin-top: 1rem;
      margin-left: 1rem;
    height: 6rem;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: start;
  }
  .c0 { background: #eee }
  .c1 { background: rgb(199, 227, 143) }
  .c2 { background: rgb(125, 200, 115) }
  .c3 { background: rgb(42, 153, 64) }
  .c4 { background: rgb(29, 96, 42) }
</style>

<!-- <progress value={$progress}></progress> -->
<!-- <Spring /> -->

<!-- <input type="text" bind:this={boxInput}>
<button on:click={addBox}>Add</button> -->

<section class="year">
  {#each boxes as box (box)}
    <div class="c2" transition:scale={{ duration: 1 }}></div>
  {/each}
</section>
