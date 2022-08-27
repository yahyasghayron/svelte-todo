<script lang="ts">
  import { onMount } from "svelte";
  import axios from "axios";
  interface Todos {
    id: number;
    todo: string;
    done: boolean;
  }
  let todos: Todos[] = [];
  onMount(async () => {
    const res = await axios.get("http://localhost:4050/api/todos");
    todos = res.data;
  });
  function deleteTodo(id: number) {
    console.log(id);
  }
</script>

<main>
  <h1>todos</h1>
  {#each todos as t}
    <div class="todo">
      <h3>{t.todo}</h3>
      <div on:click={deleteTodo(t.id)}>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </div>
    </div>
  {/each}
</main>

<style>
  .todo {
    height: 40px;
    display: flex;
    width: 100%;
    margin-bottom: 10px;
    padding: 10px 20px;
    background-color: gray;
    align-content: space-between;
  }
  .todo div svg {
    height: 20px;
  }
  .todo div {
    padding: 10px;
    border-radius: 100px;
    background-color: pink;
  }
</style>
