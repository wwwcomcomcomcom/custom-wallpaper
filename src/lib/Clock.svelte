<script lang="ts">
    let time = "00:00:00"

    function refeshTime() {
        const date = new Date();
        time = `${date.getHours().toString().padStart(2,"0")}:${date.getMinutes().toString().padStart(2,"0")}:${date.getSeconds().toString().padStart(2,"0")}`;
    }
    refeshTime();
    setInterval(refeshTime,1000);
</script>

<div class="clock">
    <span id="clock">{time}</span>
</div>

<style>
    .clock {
        z-index: 1;
        font-size: 7rem;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
</style>

