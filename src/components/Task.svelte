<script>
	export let task;

	export let toggleCheckbox;
	export let deleteTask;
</script>

<div>
	<input type="checkbox" checked={task.completed} on:click={() => toggleCheckbox(task)}>

	{task.name}

	<button on:click={() => deleteTask(task)}>delete</button>
</div>
