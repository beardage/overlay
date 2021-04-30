 <script>
    import { createEventDispatcher } from 'svelte';
    export let task;
 </script>
 

<div class="task">
    <input bind:checked={task.status} type="checkbox">
    <span class:checked={task.status}>{task.content}</span>
</div>
<div class="sub-tasks">
    {#each task.subTasks as subTask, index (subTask.id)}
        <div class="sub-task">
            <input bind:checked={subTask.status} type="checkbox">
            <span class:checked={subTask.status}>{subTask.content}</span>
        </div>
    {/each}
</div>

<style>
.task {
    background-color: #6272a4;
    border-radius: 2px;
    border: 4px solid #8be9fd;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    color: #f8f8f8;
    padding: 10px;
    margin-bottom: 10px;
}
.sub-task {
    background-color: #6272a4;
    border-radius: 2px;
    border: 4px solid #8be9fd;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    color: #f8f8f8;
    font-size: .8em;
    padding: 10px;
    margin-left: 15px;
    margin-bottom: 10px;
}
</style>
