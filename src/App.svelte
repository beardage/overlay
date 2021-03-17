<script>
    let newItem = '';

    let todoList = [
        {content: 'test item', status: false},
        {content: 'test item #2', status: false},
    ];
    
    function addToList() {
        todoList = [...todoList, {content: newItem, status: false}];
        newItem = '';
    }
    
</script>

<input bind:value={newItem} type="text" placeholder="new todo item">
<button on:click={addToList}>Add</button>

<hr>

{#each todoList as item, index}
    <input bind:checked={item.status} type="checkbox">
    <span class:checked={item.status}>{item.content}</span>
    <br>
{/each}

<style>
    .checked { color: green }
</style>
