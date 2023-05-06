<script>
    let id = 0;
    $: totalTodos = tasks.length;
    let tasks = '';
    function handleSubmit(txt){
        tasks = [...tasks, {id:++id, txt: txt, isCompleted: false}];
        for(let i = 0; i<tasks.length; i++){
            console.log(tasks[i]);
        }
    }
    let taskValue = '';
</script>

<h1>TODO-LIST</h1>
<div class="todoapp large">
    <form class="add-task" on:submit|preventDefault={handleSubmit(taskValue)}>
        <input type="text" bind:value = {taskValue} />
        <button type="submit">추가하기</button>
    </form>
    <div class="todo-list">
        <ul>
            {#each tasks as task}
            {#if task.isCompleted == false}
            <li>[{task.id}] {task.txt}</li>
            {/if}
            {/each}
        </ul>
    </div>
</div>