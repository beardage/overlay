 <script>
    export let task = {};
    export let subtasks = [];
 </script>
 

 <div class="task">
    <input bind:checked={task.status} type="checkbox">
    <span class:checked={task.status}>{task.content}</span>
    <button on:click={addSubTask}>+</button>
</div>      
