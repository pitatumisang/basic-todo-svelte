<script>

	import Todo from './Todo.svelte'
	import {todoList} from './store/todoStore.js'
 
	let todoText = '';
	let isEmpty = false;


	const handleSubmit = () => {
		if(todoText.trim() === ''){
			isEmpty = true;
			return;
		}
		
		const todo = {
			id: Date.now(),
			desc: todoText,
			completed: false
		}
		todoList.update((currentTodo) => [todo, ...currentTodo]);

		todoText = '';
	}

</script>

<main>
	<h1>todo app</h1>
	<form on:submit|preventDefault={handleSubmit}>
		<div class:empty={isEmpty} class="form-control">
			<label for="text">Todo</label>
			<input type="text" name="text" id="text" bind:value={todoText}>
		</div>
		<button>Submit</button>
	</form>

	<Todo/>
	
</main>

<style>

	main{
		max-width: 600px;
		margin: 0 auto;
	}

	h1{
		text-transform: uppercase;
		text-align: center;
		margin-top:20px;
	}

	.form-control{
		margin: 15px 0;
	}

	label{
		display: inline-block;
		font-weight: 600;
		margin-bottom: 5px;
	}

	input{
		width: 100%;
		padding:10px;
		border-radius: 5px;
		border: 1px solid rgba(0,0,0,0.3);
		font-family: 'Open sans', sans-serif;
		font-size: 15px;
	}

	.empty input{
		border: 1px solid #DC2626;
	}

	input:focus{
		outline: none;
		border: 1px solid rgba(0,0,0,0.6);
	}

	button{
		width: 100%;
		padding: 10px 0;
		cursor: pointer;
		background-color: #2563EB;
		letter-spacing: 1px;
		text-transform: uppercase;
	}

	button:hover{
		background-color:#1E40AF;
	}
	
</style>