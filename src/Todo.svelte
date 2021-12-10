<script>
    import {todoList} from './store/todoStore';

    const deleteTodo = (id) => {
        todoList.update((curr) => {
            return $todoList.filter(todo => todo.id !== id);
        })
    }

    const updateTodo = (id) => {    
        todoList.update(currentTodos => {
            const idx = currentTodos.findIndex(todo => todo.id === id);

            currentTodos[idx].completed = !currentTodos[idx].completed;

            return currentTodos;
        })
    }

</script>

{#if $todoList.length === 0}
    <h3>There are no todos yet!</h3>
{:else}
    {#each $todoList as todo}
    <li>
        <input type="checkbox" checked={todo.completed} on:change={() => { updateTodo(todo.id)}}>
        <span class={todo.completed === true ? 'complete' : ''}>{todo.desc}</span>
        <button on:click={() => {deleteTodo(todo.id)}}>Delete</button>
    </li>
    {/each}

{/if}

<style>
    h3{
        text-align: center;
        margin-top: 10px;
    }
    li{
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        list-style:  none;
        margin-top: 15px;
        border: 1px solid rgba(0,0,0,0.1);
        border-radius: 5px;
        padding: 10px;
    }

    li span{
        flex: 1;
        margin-left: 10px;
    }

    button{
		background-color: #DC2626;
        padding: 5px;
	}
    button:hover{
		background-color:#991B1B;
	}

    .complete{
        text-decoration: line-through;
    }
</style>