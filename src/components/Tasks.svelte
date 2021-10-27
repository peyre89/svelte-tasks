<script>
	export let tasks = [];

	const FILTER_ALL = 'all';
	const FILTER_ACTIVE = 'active';
	const FILTER_COMPLETED = 'completed';

	let newTaskName = '';

	$: newTaskId = tasks.length === 0 ? 1 : Math.max(...tasks.map(t => t.id)) + 1;

	const addTask = () => {
		tasks = [
			...tasks,
			{
				id: newTaskId,
				name: newTaskName,
				completed: false
			}
		];

		newTaskName = '';
	}

	const deleteTask = task => {
		tasks = tasks.filter(t => t.id !== task.id);
	}

	let filter = FILTER_ALL;

	const filterTasks = (filter, tasks) => {
		if (filter === FILTER_ACTIVE) {
			return tasks.filter(t => t.completed === false);
		}

		if (filter === FILTER_COMPLETED) {
			return tasks.filter(t => t.completed === true);
		}

		return tasks;
	}

	const toggleCheckbox = task => {
		tasks = tasks.map(t => {
			if (t.id === task.id) {
				return {
					...task,
					completed: !t.completed
				}
			}

			return t;
		});
	}
</script>

<div>
	<form on:submit|preventDefault={addTask}>
		<label for="task">New task?</label>
		<input id="task" bind:value={newTaskName} />

		<button type="submit">Add</button>
	</form>

	<div class="filters">
		<button class:active={filter === FILTER_ALL} on:click={() => filter = FILTER_ALL}>All</button>
		<button class:active={filter === FILTER_ACTIVE} on:click={() => filter = FILTER_ACTIVE}>Active</button>
		<button class:active={filter === FILTER_COMPLETED} on:click={() => filter = FILTER_COMPLETED}>Completed</button>
	</div>

	<ul>
		{#each filterTasks(filter, tasks) as task (task.id)}
			<li>
				<input type="checkbox" checked={task.completed} on:click={() => toggleCheckbox(task)}>

				{task.name}

				<button on:click={() => deleteTask(task)}>delete</button>
			</li>
		{/each}
	</ul>
</div>

<style>
	form {
		margin-top: 48px;
	}

	input {
		margin-top: 12px;
	}

	.filters {
		margin-top: 32px;
	}

	.active {
		background-color: #ffe3b8;
	}

	button + button {
		margin-left: 8px;
	}

	ul {
  		list-style: none;
  		padding: 0;

		margin-top: 40px;
	}
</style>
