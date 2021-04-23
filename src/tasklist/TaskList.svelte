<script>
   import { createEventDispatcher } from 'svelte';
   import { onMount } from 'svelte';
   import Task from './Task.svelte';
   
   const dispatch = createEventDispatcher();
   let newItem = '';
   $: taskList = [];

   onMount(async () => {
      const interval = setInterval(async () => {
         const res = await fetch(`http://localhost:3000/todos`);
         taskList = await res.json();      
      }, 2000);
      return () => clearInterval(interval);
   });

   function addToList() {
      //taskList = [...taskList, {id: generateId(), content: newItem, status: false, editing: false, subTasks: []}];
      //newItem = '';   
   }

   function addSubTask(task) {
      //task.subTasks.push({id:generateId(), content: newSubTask, status: false, editing: true});
      //let index = taskList.findIndex((taskToUpdate) =>
         //taskToUpdate.id === task.id);
      //taskList[index] = task;
   }
  
   function removeSubTask(task, subTaskId) {
      //let taskIndex = taskList.findIndex((taskToAlter) =>
            //taskToAlter.id === task.id);  
      //let subTaskIndex = taskList[taskIndex].subTasks.findIndex((subTaskToRemove) =>
         //subTaskToRemove.id === subTaskId);
      //taskList[taskIndex].subTasks.splice(subTaskIndex, 1);
      //taskList = taskList;
   }
     
   function removeTask(task) {                                                                                                         
      //let index = taskList.findIndex((taskToRemove) =>
         //taskToRemove.id === task.id);
      //taskList.splice(index, 1);
      //taskList = taskList;
   }
       
   function updateTask(task) {
      //let index = taskList.findIndex((taskToUpdate) =>
        // taskToUpdate.id === task.id);
      //taskList[index] = task;
   }
      
   function handleAddSubTask(event) {
      //addSubTask(event.detail);
   }
      
   function handleEditTask(event) {
      //updateTask(event.detail);
   }
  
   function handleRemoveTask(event) {
      //removeTask(event.detail); 
   }
      
   function handleRemoveSubTask(event) {
     // removeSubTask(event.detail.task, event.detail.subTaskId);
   }
      
   function generateId() {
      return Date.now() + (Math.random() * 1000);
   }

</script>

<div class="task-list">
   {#each taskList as task, index (task.id)}
      <div class="task-container">
         <Task {task} on:addSubTask={handleAddSubTask} on:editTask={handleEditTask} on:removeTask={handleRemoveTask} on:removeSubTask={handleRemoveSubTask}/>
      </div>
   {:else}
      <p>loading</p>
   {/each}
</div>

<style>
   .task-list {
      position: absolute;
      top: 10px;
      right: 10px;
      max-width: 375px;
   }
</style>
