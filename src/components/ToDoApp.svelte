<script>
	import {onMount} from 'svelte';
    import ToDoControls from './ToDoControls.svelte';
    import ToDoitem from './ToDoitem.svelte';
let items=[];
let id=0;  
onMount(()=>{
    if(localStorage.key('items')){
        items=JSON.parse(localStorage.getItem('items'));
    }
    if (items.length){
    items.forEach((i)=>{
        if(id< i.id){
            id=i.id;
        }
    });
    id++;
}
    }); 
function onChangeStatus(event){
    const item=items.find((i)=> i.id===event.detail.id);
    item.isDone =!item.isDone;
    items= items;
    localStorage.setItem('items',JSON.stringify(items));
}

function onAddItem(event){
    const item={
    id:id++,
    text:event.detail.text,
    isDone:false
};
    items.push(item);
    items=items;
    localStorage.setItem('items',JSON.stringify(items));
}
function onDeleteItem(event){
    const idx=items.findIndex(i=>i.id===event.detail.id);
    items.splice(idx,1);
    items=items;
    localStorage.setItem('items',JSON.stringify(items));
}
</script>
<div class="todo_app">
    <ToDoControls on:add={onAddItem}/>
    <div class="todo_app_field">
        {#each items as item}
        <ToDoitem 
        id={item.id}
        text={item.text} 
        isDone={item.isDone}
        on:change={onChangeStatus}
        on:remove={onDeleteItem}/>  
    {/each}
    </div>
</div>
<style>
    .todo_app{
    background: #35d1bc;
    border-radius: 15px;
    height: 70%;
    width: 500px;
    padding: 40px 60px;
    display: flex;
    flex-direction: column;
    gap:20px;
}
.todo_app_field{
    background: white;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 20px;
    flex-grow: 1;
    overflow-y: auto;
}
</style>