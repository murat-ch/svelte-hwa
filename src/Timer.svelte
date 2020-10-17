<script>
    import ProgressBar from './ProgressBar.svelte';

    const totalSeconds = 20;
    let secondLeft = totalSeconds;
    let isRunning = false;
    function startTimer() {
        isRunning = true;
        let timer = setInterval(() => {
            secondLeft = secondLeft - 1;
            if (secondLeft === 0) {
                clearInterval(timer);
                isRunning = false;
                secondLeft = totalSeconds;
            }
        }, 1000);
    }

</script>
<style>
    h2 {
        margin: 0;
    }
    .start {
        background-color: rgb(154, 73, 73);
        width: 100%;
        margin: 10px 0;
    }
    .start[disabled] {
        background-color: rgb(194, 194, 194);
        cursor: not-allowed;
    }
</style>
<div bp="grid">
    <h2 bp="offset-5@md 4@md 12@sm">
        Seconds Left: {secondLeft}
    </h2>
</div>
<ProgressBar progress="{(totalSeconds - secondLeft)*100/totalSeconds}"/>
<div bp="grid">
    <button class="start" bp="offset-5@md 4@md 12@sm" disabled={isRunning} on:click={startTimer}>
        Start
    </button>
</div>
