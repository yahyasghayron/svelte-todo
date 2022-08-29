<script lang="ts">
  import { onMount } from "svelte";
  import axios from "axios";
  import AddTodo from "./lib/AddTodo.svelte";
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
  async function deleteTodo(id: number) {
    const res = await axios.delete("http://localhost:4050/api/todos/" + id);
    todos = res.data;
  }
  async function refrechTodos(event: any) {
    todos = event.detail.todos;
  }
  async function marckDone(id: number) {
    const res = await axios.patch(
      "http://localhost:4050/api/todos/" + id + "/done"
    );
    todos = res.data;
  }
  async function marckUndone(id: number) {
    const res = await axios.patch(
      "http://localhost:4050/api/todos/" + id + "/undone"
    );
    todos = res.data;
  }
</script>

<main class="container">
  <h1>todos</h1>
  <AddTodo on:createTodo={refrechTodos} />
  {#each todos as t}
    <div class="todo">
      {#if t.done}
        <h3
          on:click={() => {
            marckUndone(t.id);
          }}
        >
          ✔️
          {t.todo}
        </h3>
      {/if}
      {#if !t.done}
        <h3
          on:click={() => {
            marckDone(t.id);
          }}
        >
          {t.todo}
        </h3>
      {/if}
      <div
        on:click={() => {
          deleteTodo(t.id);
        }}
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
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
    height: 50px;
    display: flex;
    margin-bottom: 10px;
    padding: 10px 20px;
    background-color: gray;
    align-content: space-between;
  }
  .todo h3 {
    width: 100%;
  }
  .todo div svg {
    height: 30px;
  }
  .todo div {
    border-radius: 100px;
    background-color: pink;
    color:white;
  }
</style>
