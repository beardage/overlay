<script>
    let newItem = '';
    let newSubTask = '';

    let taskList = [
        {id: 1, content: 'test item', status: false},
        {id: 2, content: 'test item #2', status: false},
    ];

    let subTaskList = [
        {id: 1, content: 'test subtask', status: false},
    ];
    
    function addToList() {
        taskList = [...taskList, {id: generateId(), content: taskTitle, status: false}];
        newItem = '';
    }

    function addSubTask() {
        subTaskList = [...subTaskList, {id:generateId(), content: newSubTask, status: false}];
        newSubTask = '';
    }
    
    function generateId() {
        return Date.now();
    }
    
    
</script>

<input bind:value={newItem} type="text" placeholder="new task">
<button on:click={addToList}>Add</button>

<hr>

{#each taskList as item, index}
    <div class="task-container">
        <Task class="task">
            <input bind:checked={item.status} type="checkbox">
            <span class:checked={item.status}>{item.content}</span>
            <button on:click={addSubTask}>+</button>
        </Task>
        <div class="sub-tasks">
            {#each subTaskList as item (item.id), index}
                <subTask class="sub-task">
                    <input bind:checked={item.status} type="checkbox">
                    <span class:checked={item.status}>{item.content}</span>
                </subTask>   
                {#if index == subTaskList.length-1}
                    <input bind:value={newSubTask} type="text" placeholder="new subtask">
                    <button on:click={addSubTask}>+</button>
                {/if}
            {/each}
        </div>
    </div>
{/each}

<style>
    .checked { color: green }
    .sub-tasks { 
        color: #666;
        padding-left: 15px;

    }
</style>
