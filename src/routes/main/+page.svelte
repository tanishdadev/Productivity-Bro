<script>
    let time = $state(25 * 60);
    let isRunning = false;
    let timer;

    function startTimer() {
        if (isRunning) return;
        isRunning = true;
        timer = setInterval(() => {
            if (time <= 0) {
                clearInterval(timer);
                isRunning = false;
                alert("Time's up!");
                return;
            }
            time--;
        }, 1000);
    }

    function pauseTimer() {
        if (!isRunning) return;
        clearInterval(timer);
        isRunning = false;
    }

    function resetTimer() {
        clearInterval(timer);
        time = 25 * 60;
        isRunning = false;
    }

    function toggleTheme() {
    }

</script>

<div class="flex justify-end px-5">
    <button class="border-2">Toggle Screen</button>
</div>

<div class="space-y-20 py-50 flex flex-col items-center justify-center">
    <div class="flex flex-col items-center justify-center">
        <h1 class="text-8xl">{Math.floor(time/60)}:{String(time%60).padStart(2,'0')}</h1>
    </div>

    <div class="space-x-20">
        <button onclick={startTimer} class="border-2">Start</button>
        <button onclick={pauseTimer} class="border-2">Pause</button>
        <button onclick={resetTimer} class="border-2">Reset</button>
    </div>
</div>

<style>

</style>