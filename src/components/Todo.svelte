<script>
    let id = 0;
    let tasks = '';
    const pushTask = (title)=>{
        tasks = [...tasks, {id:++id, title: title, isCompleted: false, isShow:true}];
    }
    let taskValue = '';
    
    //get date
    const date = new Date();
    let year = date.getFullYear();
    let month = date.getMonth()+1;
    let day = date.getDay();
    let stringDate = year+'.'+month+'.'+day;
    
    //handle user comment
    let userComment = "화이팅!";

    //delte comment
    const delteCheckedBlock = ()=>{
        for(let i = 0; i<tasks.length; i++){
            if(tasks[i].isCompleted == true){
                tasks[i].isShow = false;
                //tasks = tasks;
            }
        }
    }
</script>

<hr>
<h1 class="display-date">
    {stringDate}
</h1>
<hr>
<h1 class="display-comment">{userComment}</h1>
<hr>
<div class="display-tasks">
    <form class="add-task" on:submit|preventDefault={pushTask(taskValue)}>
        <input type="text" bind:value = {taskValue} />
        <button type="submit">+</button>
    </form>
    <div class="todo-list">
        {#each tasks as task}
        {#if task.isCompleted == false && task.isShow == true}
        <div class="task-box uncompleted-block" id = "task{task.id}">
            <div class="task-title">{task.title}</div>
            <input type="checkbox" bind:checked={task.isCompleted}>
        </div>
        {:else if task.isShow == true}
        <div class="task-box completed-block" id="task{task.id}">
            <div class="task-title"><strike>{task.title}</strike></div>
            <input type="checkbox" bind:checked={task.isCompleted}>
        </div>
        {/if}
        {/each}
    </div>
    <button on:click={()=>{delteCheckedBlock()}}>clean</button>
</div>