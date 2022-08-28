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
}
</script>
<div>
<input bind:value="{todo}" type="text">
<button on:click="{createTodo}">
add todo
</button>
</div>
