<script>
    import{createEventDispatcher} from 'svelte';
    const dispatch=createEventDispatcher()
    let inputValue='';
    function onClick(){
        if(inputValue.length){
            dispatch('add',{text:inputValue});
            inputValue='';
        }
    }
    function handlekeydown(e){
        if (e.key === 'Enter'&& inputValue.length) {
    }
}
</script>
<div class="todo_app_controls">
    <input class="todo_app_input" type="text" bind:value={inputValue}/>
    <button class="todo_app_button" on:click={onClick} on:keydown={handlekeydown}>add</button>
</div>
<style>
.todo_app_controls{
    display: grid;
    grid-template-columns: 70% 30%;
}
.todo_app_input{
    border:none;
    border-radius: 15px 0 0 15px;
    padding: 20px 10px;
}
.todo_app_button{
    background: #FBCC28;
    border-radius: 0 15PX 15PX 0;
    border:none;
}
</style>