<script>
	export let tasks = [];
	let newTask = "";
	let checkAllState = false;
	const MAX_TASKS = 50;

	function addTask() {
		if (!newTask.trim()) return;
		if (tasks.length >= MAX_TASKS) {
			alert(`You can only add up to ${MAX_TASKS} tasks.`);
			return;
		}
		tasks = [...tasks, { text: newTask.trim(), done: false }];
		newTask = "";
	}

	function toggleTask(index) {
		tasks[index].done = !tasks[index].done;
		tasks = [...tasks];
	}

	function checkAll() {
		checkAllState = !checkAllState;
		tasks = tasks.map(task => ({ ...task, done: checkAllState }));
	}

	function removeAll() {
		tasks = [];
		checkAllState = false;
	}
</script>

<div class="p-4 w-75 font-sans border border-black">
	<h2 class="text-center mb-3">To-Do List</h2>

	<!-- Input and Add Button -->
	<div class="flex gap-4 mb-5">
		<input
			type="text"
			bind:value={newTask}
			placeholder="Add a new task"
			class="border border-black px-2 py-1 flex-1 focus:outline-none"
			on:keydown={(e) => e.key === "Enter" && addTask()}
		/>
		<button class="border border-black px-3 py-1" on:click={addTask}>
			Add
		</button>
	</div>

	<!-- Task List -->
	<div class="border border-black p-1 max-h-40 overflow-y-auto">
		<ul class="space-y-1">
			{#each tasks as task, i}
				<li class="flex justify-between items-center border-b border-black last:border-b-0 py-1 px-1">
					<span class={task.done ? "line-through" : ""}>{task.text}</span>
					<input
						type="checkbox"
						checked={task.done}
						on:change={() => toggleTask(i)}
					/>
				</li>
			{/each}
		</ul>
	</div>

	<!-- Action Buttons -->
	<div class="flex gap-2 mt-3">
		<button class="border border-black px-2 py-1 flex-1" on:click={checkAll}>
			{checkAllState ? "Uncheck all" : "Check all"}
		</button>
		<button class="border border-black px-2 py-1 flex-1" on:click={removeAll}>
			Remove all
		</button>
	</div>
</div>
