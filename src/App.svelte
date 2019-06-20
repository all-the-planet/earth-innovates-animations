<script>
    import { writable } from "svelte/store";

    const progress = writable(0);
</script>

<progress value={$progress}></progress>



