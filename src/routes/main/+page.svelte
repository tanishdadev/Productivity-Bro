<script>
    import ToDo from './ToDo.svelte';
    import Settings from './settings.svelte'
    import { onMount } from 'svelte';
    let isSettingsOpen = $state(false);
    let time = $state(25 * 60);
    let isRunning = false;
    let timer;
    let isDropDownOpen = $state(false);
    let name = "User";
    let showList = $state(false);
    let quote = $state('');
    let author = $state('');
    let audio;
    let musicOn = $state(localStorage.getItem("musicOn") !== "false");

    onMount(() => {
	    const startMusic = sessionStorage.getItem("startMusic") === "true";

	    if ((startMusic || musicOn) && audio) {
		    audio.play().catch(e => {
			    console.warn("Autoplay blocked by browser:", e);
		    });
	    }

	    sessionStorage.removeItem("startMusic");
    });


    async function fetchQuote() {
        try{
            const response = await fetch('https://proxymad.vercel.app/api/proxy?url=https://zenquotes.io/api/random');
            const data = await response.json();
            quote = data[0].q;
            author = data[0].a;
        } catch (error) {
            console.error('Error fetching quote:', error);
            quote = 'Don’t let the noise of others’ opinions drown out your own inner voice.';
            author = 'Steve Jobs';
        }
    }
    fetchQuote();

    function toggleMusic() {
	    musicOn = !musicOn;
	    localStorage.setItem("musicOn", musicOn);

	    if (musicOn) {
		    audio.play().catch(e => console.warn("Couldn't play:", e));
	    }
        else {
		    audio.pause();
	    }
    }

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

<audio src="/music.mp3" bind:this={audio} preload="auto" loop></audio>

<div class={isSettingsOpen ? 'blur-sm pointer-events-none select-none' : ''}>
    <div class="flex justify-end px-5 gap-x-5">
        <div class="relative">
        <button onclick={toggleDropDown} class="border-2">Open menu</button>

        {#if isDropDownOpen}
            <div class="absolute top-10 w-45 bg-blue-200 text-lg text-black rounded-sm shadow-lg z-1">
                <button class="block px-4 py-2 hover:bg-gray-100 w-full">To-do List</button>
                <button class="block px-4 py-2 hover:bg-gray-100 w-full">Shuffle Quote</button>
                <button class="block px-4 py-2 hover:bg-gray-100 w-full">Enable Bunny</button>
                <button onclick={() => { isSettingsOpen = true; isDropDownOpen = false }} class="block px-4 py-2 hover:bg-gray-100 w-full">Settings</button>
            </div>
        {/if}
        </div>

        <button class="border-2">Toggle Theme</button>
    </div>

    <div class="absolute top-[350px] left-25 z-1">
        <ToDo/>
    </div>

    <div>
        <div class="absolute top-2 left-1/2 transform -translate-x-1/2 text-center space-y-2">
            <div class="">{quote}</div>
            <div class="">- {author}</div>
        </div>

        <div>
            <div class="text-3xl text-center absolute w-full top-30">Good Day, {name}</div>
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
</div>

{#if isSettingsOpen}
    <Settings close={() => isSettingsOpen = false} toggleMusic={toggleMusic} musicOn={musicOn}/>
{/if}

<style>

</style>