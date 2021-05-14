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
</script>

<div class="task-list">
   {#each taskList as task, index (task._id)}
      <div class="task-container">
         <Task {task}/>
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
