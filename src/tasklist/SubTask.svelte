<style>
.subtask {
    color: #cecece;
}
</style>

<SubTask class="sub-task">
    <input bind:checked={subTask.status} type="checkbox">
    <span class:checked={subTask.status}>{subTask.content}</span>
    {#if index == subTaskList.length-1}                                                 
        <input bind:value={newSubTask} type="text" placeholder="new subtask">
        <button on:click={addSubTask}>+</button>
    {/if}
</SubTask>   
