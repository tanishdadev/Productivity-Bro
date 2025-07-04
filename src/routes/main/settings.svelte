<script>
	export let close;
	export let musicOn;
	export let toggleMusic;

    function changeBackground() {
        // background change logic here
    }
</script>

<div class="fixed inset-0 bg-black/20 backdrop-blur-sm flex items-center justify-center z-50">
    <div class="bg-white p-6 rounded-lg shadow-lg w-96 text-center">
        <h2 class="text-2xl font-bold mb-4">Settings</h2>
        <p class="mb-5 text-gray-800">Customize your experience</p>
        <p>Music: <button onclick={toggleMusic} class="p-1 ml-[15px] rounded {musicOn ? 'bg-green-500' : 'bg-red-500'} hover:cursor-pointer">{musicOn ? 'On' : 'Off'}</button></p>
        <p>Choose background: <button onclick={changeBackground} class="bg-gray-400 rounded my-5 ml-[15px] p-1 hover:cursor-pointer">Select</button></p>

        <button class="mt-4 px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700" onclick={close}>Close</button>
    </div>
</div>