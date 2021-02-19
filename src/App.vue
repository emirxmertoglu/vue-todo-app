<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent>
    <label>New Todo</label> <br />
    <input type="text" v-model="todo" autofocus />
    <button class="btn" @click="addNewTodo">Add New Todo</button>
    <button class="btn">Remove All Todos</button>
    <button class="btn">Mark All Todos Done</button>
  </form>
  <ul>
    <li class="todo" v-for="todo in todos" :key="todo.content">
      <h3>{{ todo.content }}</h3>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";
export default {
  name: "App",
  setup() {
    const todo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        content: todo.value,
        done: false,
      });
      todo.value = "";
    }

    return { todo, todos, addNewTodo };
  },
};
</script>

<style>
#app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  width: 1200px;
  margin: 40px auto;
  text-align: center;
}

.btn {
  display: block;
  margin: 10px auto;
  padding: 10px;
  border: none;
  background: #eee;
  color: #212121;
  width: 170px;
  border-radius: 10px;
  font-weight: 600;
}

label {
  font-size: 1.2em;
  font-weight: 700;
}

input {
  width: 230px;
  margin: 10px;
  padding: 5px;
}

.todo {
  list-style: none;
}

.todo h3 {
  margin-left: -30px;
}
</style>
