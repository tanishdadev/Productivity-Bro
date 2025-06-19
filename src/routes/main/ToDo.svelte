<script>

</script>

<div>
    <form>
        <h1>What needs to be done?</h1>
        <input type="text" name="addTask" id="addTask" placeholder="Add a new task" class="border-2 p-2 rounded-md w-full mb-4">
        <button class="border-5 h-full w-full">Add</button>
        <div id="taskList">
            <ul>
                <li class="flex justify-between items-center border-b-2 py-2">
                    <input type="checkbox" name="" id="" class="border-none rounded-2xl focus:outline-none outline-none active:outline-none focus:ring-0 ring-0 active:ring-0">
                    <span>Sample Task 1</span>
                </li>
                <li class="flex justify-between items-center border-b-2 py-2">
                    <span>Sample Task 2</span>
                    <button class="border-2 px-2">Done</button>
                </li>
            </ul>
        </div>
        <div class="flex justify-between mt-2">
            <button class="border-4 mt-5">Check all</button>
            <button class="border-4 mt-5">Remove all</button>
        </div>
    </form>
</div>

<style>

</style>