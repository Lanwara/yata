<script lang="ts">
	type Todo = { id: number; text: string; isComplete: boolean };

	let todos = $state<Todo[]>([
		{ id: 0, text: "My first todo", isComplete: false },
	]);

	let textInput = $state("");

	function handleAdd() {
		const nextId = todos.length;

		todos.push({ id: nextId, text: textInput, isComplete: false });
	}

	function toggleCompletionState(todoIndex: number) {
		todos[todoIndex].isComplete = !todos[todoIndex].isComplete;
	}
</script>

<h1>Yet Another fucking to-do app</h1>

<h2>Add todo</h2>

<form>
	<input type="text" bind:value={textInput} />
	<button type="submit" onclick={() => handleAdd()}>Add</button>
</form>

<h2>Todos</h2>
<ol>
	{#each todos as todo (todo.id)}
		<li class:completed={todo.isComplete}>
			<input type="checkbox" onclick={() => toggleCompletionState(todo.id)} />
			{todo.text}
		</li>
	{/each}
</ol>

<style>
	li.completed {
		text-decoration: line-through;
	}
</style>
