<script>
    import ToDo from './ToDo.svelte';
    import Settings from './settings.svelte'
    import { onMount } from 'svelte';
    let isSettingsOpen = $state(false);
    let time = $state(25 * 60);
    let isRunning = false;
    let timer;
    let isDropDownOpen = $state(false);
    let name = $state("User");
    let showList = $state(false);
    let audio;
    let musicOn = $state(localStorage.getItem("musicOn") === "true");

	const firebaseConfig = {
	    apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
	    authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
	    projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
	    storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
	    messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
	    appId: import.meta.env.VITE_FIREBASE_APP_ID
	};

    onMount(async () => {
        const { initializeApp } = await import("https://www.gstatic.com/firebasejs/11.9.1/firebase-app.js");
        const { getAuth, onAuthStateChanged } = await import("https://www.gstatic.com/firebasejs/11.9.1/firebase-auth.js");
        const { getFirestore, doc, getDoc } = await import("https://www.gstatic.com/firebasejs/11.9.1/firebase-firestore.js");

	    const app = initializeApp(firebaseConfig);
	    const auth = getAuth(app);
	    const db = getFirestore(app);

	    onAuthStateChanged(auth, async (user) => {
		    if (user) {
			    const userDocRef = doc(db, "users", user.uid);  
			    const userDoc = await getDoc(userDocRef);

			    if (userDoc.exists()) {
				    name = userDoc.data().name || "User";
			    }
		    }
	    });

        const startMusic = sessionStorage.getItem("startMusic") === "true";
        if ((startMusic || musicOn) && audio) {
            audio.play()
                .then(() => {
                    musicOn = true;
                    localStorage.setItem("musicOn", true);
                })
                .catch(e => console.warn("Couldn't play:", e));
        }
        sessionStorage.removeItem("startMusic");
    });

    async function toggleMusic() {
        if (musicOn) {
            audio.pause();
            musicOn = false;
        } 
        else {
            try {
                await audio.play();
                musicOn = true;
            } catch (e) {
                console.warn("Couldn't play:", e);
                musicOn = false; // fallback in case autoplay blocked
            }
        }
        localStorage.setItem("musicOn", musicOn);
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
        <button onclick={toggleDropDown} class="border-2 mr-[120px] p-1">Open menu</button>

        {#if isDropDownOpen}
            <div class="absolute top-12 w-45 bg-blue-200 text-lg text-black rounded-sm shadow-lg z-1">
                <button onclick={toggleTodoList} class="block px-4 py-2 hover:bg-gray-100 w-full">To-do List</button>
                <button onclick={() => { isSettingsOpen = true; isDropDownOpen = false }} class="block px-4 py-2 hover:bg-gray-100 w-full">Settings</button>
            </div>
        {/if}
        </div>
    </div>

    {#if showList}
        <div class="absolute top-[350px] left-0 mx-[50px]">
            <ToDo/>
        </div>
    {/if}

    <div>
        <div>
            <div class="text-3xl text-center absolute w-full top-30">Good Day, {name}</div>
        </div>

        <div class="space-y-20 py-60 flex flex-col items-center justify-center">
            <div class="flex flex-col items-center justify-center">
                <h1 class="text-7xl">{Math.floor(time/60)}:{String(time%60).padStart(2,'0')}</h1>
            </div>

            <div class="space-x-20">
                <button onclick={startTimer} class="border-2 p-2">Start</button>
                <button onclick={pauseTimer} class="border-2 p-2">Pause</button>
                <button onclick={resetTimer} class="border-2 p-2">Reset</button>
            </div>
        </div>
    </div>
</div>

{#if isSettingsOpen}
    <Settings close={() => isSettingsOpen = false} bind:musicOn toggleMusic={toggleMusic}/>
{/if}

<style>

</style>