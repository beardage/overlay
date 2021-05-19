 <script>
    import { createEventDispatcher } from 'svelte';
    $: reportChange = function () {
             console.log('change happened');
    }
    export let task;
 </script>
 

 <div class="task {task.status}">
    <input bind:checked={task.status} type="checkbox">
    <span class:checked={task.status}>{task.content}</span>
</div>

<style lang="scss">
.task {
    background-color: #6272a4;
    border-radius: 2px;
    border: 4px solid #8be9fd;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    color: #f8f8f8;
    padding: 10px;
    margin-bottom: 10px;

    &.true {
        transition: transform ease-in-out;
        animation-name: completed;
        animation-duration: 1s;
    }
}

    @keyframes completed {
        0% {
            transform: translateX(0) scaleX(1);
        }
        50% {
            transform: translateX(-50px) scaleX(1.2);
        }
        100% {
            transform: translate(0) scaleX(1);
        }
    }




</style>
