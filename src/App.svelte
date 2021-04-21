<script>
    import TaskList from './tasklist/TaskList.svelte';
    let newItem = '';
    let newSubTask = '';

     
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

    function removeSubTask(task, subTaskId) {
        let taskIndex = taskList.findIndex((taskToAlter) =>
            taskToAlter.id === task.id);
        let subTaskIndex = taskList[taskIndex].subTasks.findIndex((subTaskToRemove) =>
            subTaskToRemove.id === subTaskId);
        taskList[taskIndex].subTasks.splice(subTaskIndex, 1);
        taskList = taskList;
    }
    
    function removeTask(task) {
        let index = taskList.findIndex((taskToRemove) =>
            taskToRemove.id === task.id);
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
    
    function handleRemoveSubTask(event) {
        removeSubTask(event.detail.task, event.detail.subTaskId);
    }
    
    function generateId() {
        return Date.now() + (Math.random() * 1000);
    }
    
    
</script>

<input bind:value={newItem} type="text" placeholder="new task">
<button on:click={addToList}>Add</button>

<TaskList/>
