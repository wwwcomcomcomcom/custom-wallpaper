<script lang="ts">
    export let index:number = 0;

    let tick = 0;
    function ticking() {
        tick++;
        if(tick > 255){
            tick = 0
        }

    }
    setInterval(ticking,30);

</script>

<div class="grid-block" id={"grid-"+index.toString()} style="--tick:{tick}">

</div>

<style>
    .grid-block {

    }
    #grid-0 {
        background: linear-gradient(135deg, rgba(255,243,0,1) 0%, rgba(255,132,0,1) 50%, rgba(255,0,254,1) 100%);
    }
    #grid-1 {
        background: linear-gradient(45deg, rgba(255,0,254,1) 0%, rgba(0,134,255,1) 50%, rgba(215,255,0,1) 100%);
    }
    #grid-2 {

    }
    #grid-3 {

    }
    #grid-4 {
        background: linear-gradient(135deg, rgba(255,0,254,1) 0%, rgba(0,172,255,1) 50%, rgba(0,255,38,1) 100%);
    }
    #grid-5 {

    }
    #grid-6 {

    }
    #grid-7 {

    }
    #grid-8 {

    }
</style>