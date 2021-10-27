<script>
	import Tasks from './components/Tasks.svelte';

	const tasks = [
		{
			id: 1,
			name: 'Sleep',
			completed: false
		},
		{
			id: 2,
			name: 'Play games',
			completed: false
		},
		{
			id: 3,
			name: 'Eat pizza',
			completed: false
		}
	];
</script>

<main>
	<h1>Tasks!</h1>

	<Tasks tasks={tasks} />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
