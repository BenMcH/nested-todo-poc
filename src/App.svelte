<script>
	import Todo from './_Todo.svelte';

	const todo = { text: '', subtasks: [], complete: false }

	let todos = [{...todo}];
</script>
<h1>Nested Todos</h1>


{#each todos as todo}
	<Todo task={todo} />
{/each}

<button on:click={() => todos = [...todos, {...todo}]}>Add Todo</button>
