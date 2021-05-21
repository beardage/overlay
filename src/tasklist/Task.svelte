 <script>
    import { createEventDispatcher } from 'svelte';
    $: reportChange = function () {
             console.log('change happened');
    }
    export let task;
 </script>
 

 <div class="task {task.status}">
    <input name="cbx" bind:checked={task.status} type="checkbox">
    <label class="checkbox" for="cbx"></label>
    <label class="label" for="cbx">{task.content}</label>
</div>

<style lang="scss">
.task {
    background-color: #6272a4;
    border-radius: 2px;
    border: 4px solid #8be9fd;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    color: #f8f8f8;
    opacity: 1;
    padding: 10px;
    margin-bottom: 10px;

    &.true {
        transition: opacity 3s ease-in-out;
        opacity: .5;
    }

    input[type="checkbox"] {
        display: none;
    }

    .checkbox {
        display: inline-block;
        position: relative;
        top: 1px;
        width: 17px;
        height: 17px;
        border: 1px solid #8be9fd;
        border-radius: 3px;
        vertical-align: middle;
        transition: background .1s ease-in-out;
        &::after {
            content: " ";
            position: absolute;
            top: 1px; 
            left: 5px;
            width: 5px;
            height: 11px;
            opacity: 0;
            transform: rotate(45deg) scale(0);
            border-right: 2px solid white;
            border-bottom: 2px solid white;
            transition: all .3s ease-in-out;
            transition-delay: .15s;
        }
    }

    .label {
        display: inline-block;
        margin-left: 5px;
        vertical-align: middle;
    }

    input[type="checkbox"]:checked ~ .checkbox {
        border-color: transparent;
        background: #8be9fd;
        animation: wiggle .6s ease;
        &::after {
            opacity: 1;
            transform: rotate(45deg) scale(1);
        }
    }
}


    @keyframes wiggle {
        from {
            transform: scale(1, 1);
        }
        30% {
            transform: scale(1.3, .7);
        }
        40% {
            transform: scale(.8, 1.2);
        }
        50% {
            transform: scale(1.1, .9);
        }
        60% {
            transform: scale(.95, 1.05);
        }
        to {
            transform: scale(1, 1);
        }
    }




</style>
