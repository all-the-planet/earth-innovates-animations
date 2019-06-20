<script>
  import { writable } from "svelte/store";
  import { tweened } from "svelte/motion";
  import { cubicIn } from "svelte/easing";
  import { fade, fly, slide, scale } from "svelte/transition";

  import Spring from "./Spring.svelte";

  //   let boxInput;

  //   const progress = tweened(0, {
  //     delay: 0,
  //     duration: 400, // default = 400
  //     easing: cubicIn
  //   });

  //   setTimeout(() => {
  //     progress.set(0.5);
  //   }, 1500);
  // for (let i = 1; i <= 5; i++) {
  //     addBox(i.toString());
  // }
  // let boxes = [{ id: 0, commit: 0 }];
  
  let boxes = [{ "id": 0, "commit": Math.floor(5 * Math.random()) }];

  function addBox(id, commit) {
    boxes = [...boxes, { "id": id, "commit": commit }];
  }

  let contrib = [];
  let i = 0;

  // add days div squares with a short delay
  let days = 336;
  setInterval(() => {
    if (i < 335) {
      i++;
      addBox(i, Math.floor(5 * Math.random()));
      // i++;
      console.log(boxes[i]);
    }
  }, 1);

  console.log(boxes[i]);
</script>

<style>
  div {
    font-size: 0.05rem;
    width: 0.48rem;
    height: 0.48rem;
    margin: 0.1rem;
    padding: 0.05rem;
  }
  .year {
    margin-top: 1rem;
    margin-left: 1rem;
    height: 5.5rem;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: start;
  }
  .c0 {
    background: #eee;
  }
  .c1 {
    background: rgb(199, 227, 143);
  }
  .c2 {
    background: rgb(125, 200, 115);
  }
  .c3 {
    background: rgb(42, 153, 64);
  }
  .c4 {
    background: rgb(29, 96, 42);
  }
  h1, h2 {
      margin-left: 1rem;
}
</style>

<!-- <progress value={$progress}></progress> -->
<!-- <Spring /> -->

<!-- <input type="text" bind:this={boxInput}>
<button on:click={addBox}>Add</button> -->
<h1>Contributions</h1>
<h2>Yearly ~ 48 work weeks</h2>
<section class="year">
  {#each boxes as box (box)}
    <div class="c{box.commit}" transition:scale={{ duration: 1 }} />
  {/each}
</section>
<h2>Daily average ~ 48 half hours</h2>
<section class="year">
  {#each boxes as box (box)}
    <div class="c{box.commit}" transition:scale={{ duration: 1 }} />
  {/each}
</section>
