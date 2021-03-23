 <script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();
    export let task;
    export let subtasks;
    
    function addSubTask() {
        dispatch('addSubTask', true);
    }
 </script>
 

<div class="task">
    <input bind:checked={task.status} type="checkbox">
    <span class:checked={task.status}>{task.content}</span>
    <button on:click={addSubTask}>+</button>
    <div class="sub-tasks">
        {#each task.subTasks as subTask, index}
            <div class="sub-task">
                <input bind:checked={subTask.status} type="checkbox">
                <span class:checked={subTask.status}>{subTask.content}</span>
            </div>
        {/each}
    </div>
</div>      

<style>
.checked { color: green; }
.sub-task {
    color: #4e4e4e;
    padding-left: 15px;
}
</style>
