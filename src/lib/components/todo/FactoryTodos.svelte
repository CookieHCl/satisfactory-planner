<script lang="ts">
	let { todos } = $props();
</script>

<div class="factory-container">
	<h3 class="factory-title">{todos.FACTORYNAME}</h3>
	<table class="todo-table">
		<thead class="todo-table-header">
			<tr>
				<th class="input-column">In 1</th>
				<th class="input-column">In 2</th>
				<th class="input-column">In 3</th>
				<th class="input-column">In 4</th>
				<th class="output-column">Out 1</th>
				<th class="output-column">Out 2</th>
				<th class="count-column">Count</th>
				<th class="checkbox-column">Done?</th>
			</tr>
		</thead>
		<tbody class="todo-table-body">
			{#each todos.todos as todo}
				<tr class="todo-row">
					<td class="input-cell"
						>{#if todo.INITEMNAME1}{todo.INITEMNAME1} {todo.INAMOUNT1 * todo.TODOAMOUNT}{/if}</td
					>
					<td class="input-cell"
						>{#if todo.INITEMNAME2}{todo.INITEMNAME2} {todo.INAMOUNT2 * todo.TODOAMOUNT}{/if}</td
					>
					<td class="input-cell"
						>{#if todo.INITEMNAME3}{todo.INITEMNAME3} {todo.INAMOUNT3 * todo.TODOAMOUNT}{/if}</td
					>
					<td class="input-cell"
						>{#if todo.INITEMNAME4}{todo.INITEMNAME4} {todo.INAMOUNT4 * todo.TODOAMOUNT}{/if}</td
					>
					<td class="output-cell"
						>{#if todo.OUTITEMNAME1}{todo.OUTITEMNAME1} {todo.OUTAMOUNT1 * todo.TODOAMOUNT}{/if}</td
					>
					<td class="output-cell"
						>{#if todo.OUTITEMNAME2}{todo.OUTITEMNAME2} {todo.OUTAMOUNT2 * todo.TODOAMOUNT}{/if}</td
					>
					<td class="count-cell">{todo.TODOAMOUNT}</td>
					<td class="checkbox-cell">
						<form method="POST" action="?/updateTodo">
							<input type="hidden" name="rowId" value={todo.ROWID} />
							<button type="submit" class="todo-save-button">Complete</button>
						</form>
					</td>
				</tr>
			{/each}
		</tbody>
	</table>
</div>

<style>
	/* Button Styling */

	.todo-save-button {
		background-color: rgba(250, 149, 73, 255);
		color: white;
		border: none;
		padding: 10px 20px;
		cursor: pointer;
		font-size: 1rem;
		border-radius: 5px;
		transition: background-color 0.3s ease;
		max-width: 100%;
	}

	.todo-save-button:hover {
		background-color: rgba(250, 149, 73, 0.8);
	}

	.todo-save-button:active {
		transform: scale(0.98);
	}

	/* Factory Container Styling */

	.factory-container {
		background-color: rgba(14, 14, 14, 255);
		border: 1px solid rgba(250, 149, 73, 255);
		margin: 20px;
		padding: 20px;
		border-radius: 10px;
	}

	.factory-title {
		color: rgba(250, 149, 73, 255);
		font-size: 1.5rem;
		margin-bottom: 10px;
	}

	/* Table Styling */

	.todo-table {
		width: 100%;
		border-collapse: collapse;
		margin-top: 10px;
	}

	.todo-table-header {
		background-color: rgba(250, 149, 73, 255);
		color: black;
	}

	.todo-table th,
	.todo-table td {
		border: 1px solid rgba(250, 149, 73, 255);
		padding: 10px;
		text-align: center;
	}

	.checkbox-column {
		width: 150px;
	}

	.input-column,
	.output-column,
	.count-column {
		padding: 10px;
	}

	.todo-table tbody tr:nth-child(even) {
		background-color: rgba(250, 149, 73, 0.1);
	}

	.todo-table-body {
		transition: background-color 0.3s ease;
	}

	.todo-table tbody tr:hover {
		background-color: rgba(250, 149, 73, 0.2);
	}

	/* Checkbox Styling */

	.checkbox-cell {
		text-align: center;
	}

	/* Input and Output Cells Styling */

	.input-cell,
	.output-cell,
	.count-cell {
		padding: 10px;
	}

	/* Responsive Styling */

	@media (max-width: 768px) {
		.factory-container {
			margin: 10px;
			padding: 15px;
		}
		.todo-save-button {
			width: 100%;
			padding: 15px;
			position: static;
			margin-bottom: 10px;
		}
		.todo-table th,
		.todo-table td {
			padding: 8px;
		}
	}
</style>
