<script>
    export let id;
    export let text;
    export let isDone;
    import{createEventDispatcher} from 'svelte';
    const dispatch=createEventDispatcher()
</script>

<div class="todo_app_item" class:todo_app_item_done={isDone}>
    <input class="todo_app_item_done" type="checkbox" 
    on:change={dispatch ('change',{id})}
    checked={isDone}
    />
    <span class="todo_app_item-text">{text}</span>
    <button class="todo_app_button" 
    on:click={dispatch ('remove',{id})}></button>
</div>
<style>
.todo_app_item{
    background: #8d4545;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
    padding: 20px;

}
.todo_app_item_done{
    background:#038810 ;
    text-decoration: line-through;
}
.todo_app_item_done .todo_app_item-text{
    text-decoration: line-through;
}
.todo_app_item-text{
    flex-grow: 1;
}  
.todo_app_button{
    border:none;
    border-radius: 30%;
    background-image:url(/img/trash2.png);
    background-repeat:no-repeat;
    height: 21px;
    width: 20px;
}
</style>