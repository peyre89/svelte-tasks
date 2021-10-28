<script>
	import Form from './Form.svelte';
	import Task from './Task.svelte';

	export let tasks = [];

	const FILTER_ALL = 'all';
	const FILTER_ACTIVE = 'active';
	const FILTER_COMPLETED = 'completed';

	$: newTaskId = tasks.length === 0 ? 1 : Math.max(...tasks.map(t => t.id)) + 1;

	const addTask = (newTaskName) => {
		tasks = [
			...tasks,
			{
				id: newTaskId,
				name: newTaskName,
				completed: false
			}
		];
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
	<Form {addTask} />

	<div class="filters">
		<button class:active={filter === FILTER_ALL} on:click={() => filter = FILTER_ALL}>All</button>
		<button class:active={filter === FILTER_ACTIVE} on:click={() => filter = FILTER_ACTIVE}>Active</button>
		<button class:active={filter === FILTER_COMPLETED} on:click={() => filter = FILTER_COMPLETED}>Completed</button>
	</div>

	<ul>
		{#each filterTasks(filter, tasks) as task (task.id)}
			<li>
				<Task {task} {toggleCheckbox} {deleteTask} />
			</li>
		{/each}
	</ul>
</div>

<style>
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
