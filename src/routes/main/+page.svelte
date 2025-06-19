<script>
    import ToDo from './ToDo.svelte';
    let time = $state(25 * 60);
    let isRunning = false;
    let timer;
    let isDropDownOpen = $state(false);
    let name = "Tanish";
    let showList = $state(false);
    let quotes = [
        "The only way to do great work is to love what you do. - Steve Jobs",
        "Life is what happens when you're busy making other plans. - John Lennon",
        "Get busy living or get busy dying. - Stephen King",
        "You have within you right now, everything you need to deal with whatever the world can throw at you. - Brian Tracy",
        "Believe you can and you're halfway there. - Theodore Roosevelt"
    ];

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
        // Code to be added for toggling theme
    }

    function toggleDropDown() {
        isDropDownOpen = !isDropDownOpen;
    }

    function toggleTodoList() {
        showList = !showList;
    }

</script>

<div class="flex justify-end px-5 gap-x-5">
    <div class="relative">
    <button onclick={toggleDropDown} class="border-2">Open menu</button>

    {#if isDropDownOpen}
        <div class="absolute top-10 w-45 bg-blue-200 text-lg text-black rounded-sm shadow-lg z-1">
			<button class="block px-4 py-2 hover:bg-gray-100 w-full">To-do List</button>
			<button class="block px-4 py-2 hover:bg-gray-100 w-full">Shuffle Quote</button>
			<button class="block px-4 py-2 hover:bg-gray-100 w-full">Enable Bunny</button>
			<button class="block px-4 py-2 hover:bg-gray-100 w-full">Settings</button>
        </div>
    {/if}
    </div>

    <button class="border-2">Toggle Theme</button>
</div>

<div class="absolute top-[350px] left-25 z-1">
    <ToDo/>
</div>

<div class="relative">
    <div>
        <div class="text-3xl text-center absolute w-full">Good Day, {name}</div>
    </div>

    <div>
        <div><!--To be added--></div>
    </div>

    <div class="space-y-20 py-60 flex flex-col items-center justify-center">
        <div class="flex flex-col items-center justify-center">
            <h1 class="text-7xl">{Math.floor(time/60)}:{String(time%60).padStart(2,'0')}</h1>
        </div>

        <div class="space-x-20">
            <button onclick={startTimer} class="border-2">Start</button>
            <button onclick={pauseTimer} class="border-2">Pause</button>
            <button onclick={resetTimer} class="border-2">Reset</button>
        </div>
    </div>
</div>


<style>

</style>