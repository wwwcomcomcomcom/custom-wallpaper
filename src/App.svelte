<script lang="ts">
import Clock from "./lib/Clock.svelte";
import GridBlock from "./lib/GridBlock.svelte";
</script>

<main>
    <Clock />
    <div class="background">
        {#each Array(9) as _, i}
            <GridBlock index={i}/>
        {/each}
    </div>
</main>

<style>
    main {
        height: 100%;
    }
    .background {
        width: 100%;
        height: 100%;
        display: grid;
        grid-template-rows: 1fr 1fr 1fr;
        grid-template-columns: 1fr 1fr 1fr;
    }
</style>
