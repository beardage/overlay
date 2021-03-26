 <script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();
    export let task;
    
    function emitAddSubTask() {
        dispatch('addSubTask', task);
    }
    
    function emitEditTask(task) {
        dispatch('editTask', task);
    }
    
    function emitRemoveTask() {
        dispatch('removeTask', task);
    }
    
    function emitRemoveSubTask(subTaskId) {
        dispatch('removeSubTask', {
            task: task,
            subTaskId: subTaskId,
        });
    }

 </script>
 

<div class="task">
    {#if task.editing}
        <input bind:value={task.content} type="text">
        <button on:click={()=>{task.editing = false; emitEditTask(task);}}>✓</button>
    {:else}
        <input bind:checked={task.status} type="checkbox">
        <span class:checked={task.status}>{task.content}</span>
        <button class="edit" on:click={()=>{task.editing = true;}}>edit</button>
        <button on:click={emitAddSubTask}>add</button>
        <button on:click={emitRemoveTask}>remove</button>
    {/if}
</div>
<div class="sub-tasks">
    {#each task.subTasks as subTask, index (subTask.id)}
        <div class="sub-task">
            <input bind:checked={subTask.status} type="checkbox">
            {#if subTask.editing}
                <input name="new-subtask" bind:value={subTask.content} placeholder="edit subtask">
                <button on:click={()=>{subTask.editing = false; emitEditTask(task);}}>✓</button>
            {:else}
                <span class:checked={subTask.status}>{subTask.content}</span>
                <button class="edit" on:click={()=>{subTask.editing = true;}}>edit</button>
                <button on:click={emitRemoveSubTask(index)}>remove</button>
            {/if}
        </div>
    {/each}
</div>

<style>
.task {
    background-color: #f2f2f2;
    border-radius: 5px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    padding: 5px;
    margin-bottom: 10px;
}
.sub-task {
    background-color: #f2f2f2;
    border-radius: 5px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    font-size: .8em;
    padding: 5px;
    margin-left: 15px;
    margin-bottom: 10px;
}
.task button, .sub-task button {
    background: none;
    border: 0;
    cursor: pointer;
    display: none;
    padding: 0 0 0 10px;
    margin: 0;
}
.task:hover button, .sub-task:hover button {
    color: darkseagreen;
    display: inline;
}
.task:hover button:hover, .sub-task:hover button {
    color: darkgreen;
}
</style>
