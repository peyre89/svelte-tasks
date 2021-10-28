<script>
	export let addTask;

	let newTaskName = '';

	function onSubmit() {
		if (newTaskName.trim() === '') {
			return;
		}

		addTask(newTaskName);
		newTaskName = '';
	}
</script>

<form on:submit|preventDefault={onSubmit}>
	<label for="task">New task?</label>
	<input id="task" bind:value={newTaskName} />

	<button type="submit">Add</button>
</form>

<style>
	form {
		margin-top: 48px;
	}

	input {
		margin-top: 12px;
	}
</style>
