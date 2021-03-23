<script>
    import Task from './tasklist/Task.svelte';
    let newItem = '';
    let newSubTask = '';
    let subTaskList = [];

    let taskList = [
        {
            id: 1, 
            content: 'test item', 
            status: false, 
            subTasks: [
                {
                    id: 1,
                    content: 'test subtask',
                    status: false
                },
                {
                    id: 2,
                    content: 'test subtask 2',
                    status: false
                },
            ] 
        },
        {
            id: 2, 
            content: 'test item 2', 
            status: false, 
            subTasks: [
                {
                    id: 1,
                    content: 'test subtask again',
                    status: false
                },
                {
                    id: 2,
                    content: 'test subtask again 2',
                    status: false
                },
            ] 
        },
    ];

    
    function addToList() {
        taskList = [...taskList, {id: generateId(), content: newItem, status: false, subTasks: []}];
        newItem = '';
    }

    function addSubTask() {
        subTaskList = [...subTaskList, {id:generateId(), content: newSubTask, status: false}];
        newSubTask = '';
    }
    
    function handleAddSubTask(event) {
        addSubTask();
    }
    
    function generateId() {
        return Date.now();
    }
    
    
</script>

<input bind:value={newItem} type="text" placeholder="new task">
<button on:click={addToList}>Add</button>

<hr>

{#each taskList as task, index}
    <div class="task-container">
        <Task {task} on:addSubTask={handleAddSubTask}/>
    </div>
{/each}

<style>
    .checked { color: green }
    .sub-tasks { 
        color: #666;
        padding-left: 15px;

    }
</style>
