<script>
    import { writable } from "svelte/store";
    import { tweened } from "svelte/motion";
    import { cubicIn } from "svelte/easing";

    import Spring from "./Spring.svelte";

    const progress = tweened(0, {
        delay: 0,
        duration: 400,   // default = 400
        easing: cubicIn
    });

    setTimeout(() => {
        progress.set(0.5);
    }, 1500);

    let boxes = ['Apples', 'Bananas', 'Oranges'];
</script>

<style>
    div {
        width: 10rem;
        height: 10rem;
        background: #ccc;
        margin: 1rem;
        box-shadow: 0 2px 8px rgba(0,0,0,0.26);
        border-radius: 5px;
        padding: 1rem;
    }
</style>

<!-- <progress value={$progress}></progress> -->
<!-- <Spring /> -->

{#each boxes as box (box)} 
    <div>{box}</div>
{/each}