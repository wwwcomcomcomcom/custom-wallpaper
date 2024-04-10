<script lang="ts">
    export let index:number = 0;

    let ticks = [255,0,0];
    let tickForward = [0,1,0];
    const tickRate = 2;
    function ticking() {
        for(let i = 0; i < ticks.length; i++) {
            ticks[i] += tickForward[i]*tickRate;
            if(ticks[i] > 255) {
                ticks[i] = 255;
                tickForward[i] = 0;
                tickForward[prevIndex(ticks,i)] = -1;
            }
            if(ticks[i] < 0) {
                ticks[i] = 0;
                tickForward[i] = 0;
                tickForward[prevIndex(ticks,i)] = 1;
            }
        }
    }
    function prevIndex(array:Array<any>,index:number):number{
        let result = index-1;
        if(result < 0){
            return array.length+result;
        }else{
            return result;
        }
    }
    function nextIndex():number{
        let result = index+1;
        if(result >= ticks.length){
            return result-ticks.length;
        }else{
            return result;
        }
    }
    setInterval(ticking,30);

</script>

<div class="grid-block" id={"grid-"+index.toString()} style="--tick1:{ticks[0]}; --tick2:{ticks[1]}; --tick3:{ticks[2]};">

</div>

<style>
    .grid-block {
        width: 100%;
    }
    #grid-0 {
        background: linear-gradient(135deg,
        rgba(var(--tick1),var(--tick2),var(--tick3),1) 0%,
        rgba(var(--tick3),var(--tick1),var(--tick2),1) 50%,
        rgba(var(--tick2),var(--tick3),var(--tick1),1) 100%);
    }
    #grid-1 {
        background: linear-gradient(0deg,
        rgba(var(--tick2),var(--tick3),var(--tick1),1) 0%,
        rgba(var(--tick3),var(--tick1),var(--tick2),1) 125%);
    }
    #grid-2 {
        background: linear-gradient(45deg,
        rgba(var(--tick2),var(--tick3),var(--tick1),1) 0%,
        rgba(var(--tick3),var(--tick1),var(--tick2),1) 50%,
        rgba(var(--tick1),var(--tick2),var(--tick3),1) 100%);
    }
    #grid-3 {
        background: linear-gradient(-135deg,
        rgba(var(--tick2),var(--tick3),var(--tick1),1) 0%,
        rgba(var(--tick3),var(--tick1),var(--tick2),1) 50%,
        rgba(var(--tick1),var(--tick2),var(--tick3),1) 100%);
    }
    #grid-4 {
        background: linear-gradient(180deg,
        rgba(var(--tick2),var(--tick3),var(--tick1),1) 0%,
        rgba(var(--tick3),var(--tick1),var(--tick2),1) 125%);
    }
    #grid-5 {
        background: linear-gradient(-45deg,
        rgba(var(--tick1),var(--tick2),var(--tick3),1) 0%,
        rgba(var(--tick3),var(--tick1),var(--tick2),1) 50%,
        rgba(var(--tick2),var(--tick3),var(--tick1),1) 100%);
    }
</style>