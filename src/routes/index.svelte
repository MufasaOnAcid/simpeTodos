<script>
	let todos = [];
	let task = '';
	let error = '';

	const addTask = () => {
		let newTask = {
			task: task,
			isComplete: false,
			createdAt: new Date()
		};
		if (task !== '') {
			todos = [...todos, newTask];
			error = '';
		} else {
			error = 'You have not typed anything';
		}
		task = '';
	};

	const markTaskAsComplete = (index) => {
		todos[index].isComplete = !todos[index].isComplete;
	};
	const removeTask = (index) => {
		let deleteItem = todos[index];
		todos = todos.filter((item) => item != deleteItem);
	};

	const keyIsPressed = (event) => {
		if (event.code === 'Enter') {
			addTask();
		}
	};
</script>

<div class="max-w-md lg:w-1/2 h-full my-auto flex flex-col gap-8 mx-auto">
	<div class="flex shadow-md ring-2 ring-black rounded-md items-center justify-between ">
		<input
			class="p-2 w-full rounded-tl-md outline-none rounded-bl-md"
			type="text"
			placeholder="Add a task"
			bind:value={task}
		/>
		<button class="bg-blue-400 p-2 w-1/4 rounded-tr-md rounded-br-md" on:click={addTask}>Add</button
		>
	</div>

	<div class={todos.length > 0 ? 'ring-2 ring-black rounded-md' : ''}>
		<ol class="list-decimal w-full">
			{#each todos as todo, index}
				<li
					class="flex items-center justify-between px-4 py-2 gap-4 {todo.isComplete
						? 'line-through'
						: ''}"
				>
					<span>{todo.task}</span>
					<span class="flex items-center gap-2">
						<button on:click={() => markTaskAsComplete(index)}>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								class="w-6 h-6 text-green-600"
								fill="none"
								viewBox="0 0 24 24"
								stroke="currentColor"
								stroke-width="2"
							>
								<path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
							</svg>
						</button>
						<button on:click={() => removeTask(index)}>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								class="h-6 w-6 text-red-500"
								fill="none"
								viewBox="0 0 24 24"
								stroke="currentColor"
								stroke-width="2"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
								/>
							</svg>
						</button>
					</span>
				</li>
			{/each}
			<p class="text-red-600">{error}</p>
		</ol>
	</div>
</div>

<svelte:window on:keydown={keyIsPressed} />
