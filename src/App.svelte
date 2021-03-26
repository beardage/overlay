<script>
    import Task from './tasklist/Task.svelte';
    let newItem = '';
    let newSubTask = '';

    let taskList = [
        {
            id: 1, 
            content: 'test item', 
            status: false, 
            editing: false,
            subTasks: [
                {
                    id: 1,
                    content: 'test subtask',
                    status: false,
                    editing: false
                },
                {
                    id: 2,
                    content: 'test subtask 2',
                    status: false,
                    editing: false
                },
            ] 
        },
        {
            id: 2, 
            content: 'test item 2', 
            status: false,
            editing: false,
            subTasks: [
                {
                    id: 1,
                    content: 'test subtask again',
                    status: false,
                    editing: false
                },
                {
                    id: 2,
                    content: 'test subtask again 2',
                    status: false,
                    editing: false
                },
            ] 
        },
    ];

    
    function addToList() {
        taskList = [...taskList, {id: generateId(), content: newItem, status: false, editing: false, subTasks: []}];
        newItem = '';
    }

    function addSubTask(task) {
        task.subTasks.push({id:generateId(), content: newSubTask, status: false, editing: true});
        let index = taskList.findIndex((taskToUpdate) =>
            taskToUpdate.id === task.id);
        taskList[index] = task;
    }
    
    function removeTask(task) {
        console.log(task);
        console.log(taskList);
        let index = taskList.findIndex((taskToRemove) =>
            taskToRemove.id === task.id);
        console.log(taskList);
        console.log(index);
        taskList.splice(index, 1);
        taskList = taskList;
    }
    
    function updateTask(task) {
        let index = taskList.findIndex((taskToUpdate) =>
            taskToUpdate.id === task.id);
        taskList[index] = task;
    }
    
    function handleAddSubTask(event) {
        addSubTask(event.detail);
    }
    
    function handleEditTask(event) {
        updateTask(event.detail);
    }

    function handleRemoveTask(event) {
        removeTask(event.detail); 
    }
    
    function generateId() {
        return Date.now();
    }
    
    
</script>

<input bind:value={newItem} type="text" placeholder="new task">
<button on:click={addToList}>Add</button>

<hr>

{#each taskList as task}
    <div class="task-container">
        <Task {task} on:addSubTask={handleAddSubTask} on:editTask={handleEditTask} on:removeTask={handleRemoveTask}/>
    </div>
{/each}

