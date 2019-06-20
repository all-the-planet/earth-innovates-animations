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

  // normal distribution param n[]
  const norm = [
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0.0013,
    0.0228,
    0.1587,
    0.5,
    0.8413,
    0.9772,
    0.9987,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    1,
    0.9987,
    0.9772,
    0.8413,
    0.5,
    0.1587,
    0.0228,
    0.0013,
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0
  ];

  let boxes = [{ id: 0, commit: Math.floor(5 * Math.random()) }];
  function addBox(id, commit) {
    boxes = [...boxes, { id: id, commit: commit }];
  }
  function discardBox(value) {
      boxes = boxes.filter(el => el.id !== value);
  }

  let halves = [{ id: 0, commit: Math.floor(5 * Math.random()), real: 0 }];
  function addHalf(id, commit, real) {
    halves = [...halves, { id: id, commit: commit, real: real }];
  }

  // add days div squares with a short delay
  let days = 336; // 336 = 7days * 48weeks - avg work year cycle
  let buffer = 335;

  function play() {
    let i = 0;
    // add a stream of elements
    let interval = setInterval(() => {
      if (i < 335) {
        i++;
        addBox(i, Math.floor(5 * Math.random()));
      }
      // remove first elements after buffer lenght reached 
      if (i >= 335) {
          i++;
          discardBox(i - 335);
      }
    }, 1);

    if (i >= 3 * 335) {
      return () => {
        clearInterval(interval);
      };
    }
  }

    function playReal() {
    let i = 0;
    let commits = 0;
    let normalized = 0;
    let interval = setInterval(() => {
      if (i < 335) {
        i++;
        commits = Math.floor(5 * Math.random());
        normalized = Math.floor(norm[Math.floor((i/7))%48]*commits);
        addHalf(i, commits, normalized > 0 ? 1 : 0 );
        // console.log(i/7, norm[(i/7)%48]);
      }
    }, 1);

    if (i >= 335) {
      return () => {
        clearInterval(interval);
      };
    }
  }

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
  h1,
  h2 {
    margin-left: 1rem;
  }
</style>

<!-- <progress value={$progress}></progress> -->
<!-- <Spring /> -->

<!-- <input type="text" bind:this={boxInput}>
<button on:click={addBox}>Add</button> -->
<h1>Progressive Contributions (animated)</h1>

<h2 on:click={play}>Yearly ~ 48 work weeks</h2>
<section class="year">
  {#each boxes as box (box)}
    <div class="c{box.commit}" transition:scale={{ duration: 1 }} />
  {/each}
</section>
<h2>Earth's Daily average ~ 48 half hours</h2>
<section class="year">
  {#each boxes as box (box)}
    <div class="c{box.commit}" transition:scale={{ duration: 1 }} />
  {/each}
</section>

<h2 on:click={playReal}>Individual Daily average ~ 48 half hours</h2>
<section class="year">
  {#each halves as half (half)}
    <div class="c{half.real}" transition:scale={{ duration: 1 }} />
  {/each}
</section>
