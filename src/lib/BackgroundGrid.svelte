<script>
import GridBlock from "./GridBlock.svelte";
</script>

<div class="background">
    {#each Array(9) as _, i}
        <GridBlock index={i}/>
    {/each}
</div>

<style>
    .background {
        width: 100%;
        height: 100%;
        display: grid;
        grid-template-rows: 1fr 1fr 1fr;
        grid-template-columns: 1fr 1fr 1fr;
    }
</style>