<script>
    import { comment } from "svelte/internal";

    let id = 0;
    let tasks = '';
    const pushTask = (title)=>{
        if(taskValue !=""){
            tasks = [...tasks, {id:++id, title: title, isCompleted: false, isShow:true}];
        }else{
            alert("할 일을 적어주세요!");       
        }
        if(taskValue != ""){
            taskValue = "";
        }
    }
    let taskValue = '';
    
    //get date
    const date = new Date();
    let year = date.getFullYear();
    let month = date.getMonth()+1;
    let day = date.getDate();
    let stringDate = year+'.'+month+'.'+day;
    
    //handle user comment
    let userInputComment = '';
    let isPushed = false;
    //delte comment
    const delteCheckedBlock = ()=>{
        for(let i = 0; i<tasks.length; i++){
            if(tasks[i].isCompleted == true){
                tasks[i].isShow = false;
            }
        }
    }
    const deleteTask = (idx)=>{
        console.log(idx);
        tasks[idx-1].isShow = false;
        tasks = tasks;
    }
    const cleanAllBlock = ()=>{
        for(let i = 0; i<tasks.length; i++){
            tasks[i].isShow = false;    
        }
    }
</script>

<hr>
<h1 class="display-date">
    {stringDate}
</h1>
<hr>
{#if isPushed == false}
<form class="add-   comment" on:submit|preventDefault = {()=>{isPushed = true;}}>
    <input type="text" placeholder="문구를 입력해주세요" bind:value={userInputComment}>
    <button type="submit">입력</button>
</form>
{:else}
<button on:click={()=>isPushed = false}>수정</button>
{/if}
<h1 class="display-comment">{userInputComment}</h1>
<hr>
<div class="display-tasks">
    <form class="add-task" on:submit|preventDefault={pushTask(taskValue)}>
        <input type="text" bind:value = {taskValue}/>
        <button type="submit">+</button>
    </form>
    <div class="todo-list">
        {#each tasks as task}
        {#if task.isShow == true}
        <div class="task-box uncompleted-block" id = "task{task.id}">
            <button on:click={deleteTask(task.id)}>-</button>
            {#if task.isCompleted == false}
            <div class="task-title">{task.title}</div>
            {:else if task.isCompleted == true}
            <div class="task-title"><strike>{task.title}</strike></div>
            {/if}
            <input type="checkbox" bind:checked={task.isCompleted}>
        </div>
        {/if}
        {/each}
    </div>
    <button on:click={()=>{delteCheckedBlock()}}>완료한 일 삭제</button>
    <button on:click={()=>{cleanAllBlock()}}>모두 지우기</button>
</div>