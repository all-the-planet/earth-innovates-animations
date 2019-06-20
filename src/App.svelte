<script>
    import { writable } from "svelte/store";
    import { tweened } from "svelte/motion";
    import { cubicIn } from "svelte/easing";


    const progress = tweened(0, {
        delay: 0,
        duration: 400,   // default = 400
        easing: cubicIn
    });

    setTimeout(() => {
        progress.set(0.5);
    }, 1500);
</script>

<progress value={$progress}></progress>



