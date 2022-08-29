<script lang="ts">
import axios from "axios";
import { createEventDispatcher } from 'svelte';

const dispatch = createEventDispatcher();

let todo : string = ""
// i shoul create the todo 
// and after i get the response
// i need to change the arry of todos
async function createTodo(){
const res = await axios.post("http://localhost:4050/api/todos",{todo: todo});
dispatch("createTodo",{
todos : res.data
})
todo = ""
}
</script>
<div>
<form on:submit|preventDefault="{createTodo}">
<input bind:value="{todo}" type="text">
</form>
</div>
