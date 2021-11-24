<script>
	import Blockquote from "./_Blockquote.svelte";


	export let parent = { complete: false };
	export let task = { text: '', subtasks: [], complete: false };
	export let indent = 1;

	let oldTask = { ...task };

	$: {
		if (task.complete && !oldTask.complete) {
			task.subtasks = task.subtasks.map(subtask => {
				const newTask = {...subtask, complete: true};

				return newTask;
			});
		}

		if (!task.complete && oldTask.complete) {
			parent.complete = false;
		}
		
		oldTask = { ...task };
	}
</script>

<div>
<input type="checkbox" bind:checked={task.complete}>
<input type="text" bind:value={task.text}>
<button on:click={() => {
	task.subtasks = [...task.subtasks, { text: '', subtasks: [], complete: false }];
}}>
	New sub-task
</button>
{#each task.subtasks as thisTask, index}
	<Blockquote bind:indent><svelte:self indent={indent+1} bind:task={task.subtasks[index]} bind:parent={task} /></Blockquote>
{/each}
</div>
