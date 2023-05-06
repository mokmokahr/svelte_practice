<script>
    let id = 0;
    let tasks = '';
    function handleSubmit(title){
        tasks = [...tasks, {id:++id, title: title, isCompleted: false}];
    }
    let taskValue = '';
    
    //get date
    const date = new Date();
    console.log(Date());
</script>

<h1>TODO-LIST</h1>
<div class="todoapp large">
    <form class="add-task" on:submit|preventDefault={handleSubmit(taskValue)}>
        <input type="text" bind:value = {taskValue} />
        <button type="submit">추가하기</button>
    </form>
    <div class="display-date">

    </div>
    <div class="todo-list">
        {#each tasks as task}
        {#if task.isCompleted == false}
        <div class="task-box uncompleted-block" id = "task{task.id}">
            <input type="checkbox" bind:checked={task.isCompleted}>
            <div class="task-title">{task.title}</div>
        </div>
        {:else}
        <div class="task-box completed-block" id="task{task.id}">
            <input type="checkbox" bind:checked={task.isCompleted}>
            <div class="task-title"><strike>{task.title}</strike></div>
        </div>
        {/if}
        {/each}
    </div>
</div>