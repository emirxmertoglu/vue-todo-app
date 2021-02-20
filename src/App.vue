<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent>
    <label>New Todo</label> <br />
    <input type="text" v-model="todo" autofocus />
    <button class="btn" @click="addNewTodo">Add New Todo</button>
    <button class="btn" @click="removeAllTodos">Remove All Todos</button>
    <button class="btn" @click="markAllTodosDone">Mark All Todos Done</button>
  </form>

  <label>Things Todo</label>
  <hr />
  <ul>
    <li class="todo" v-for="(todo, index) in todos" :key="todo.content">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{ todo.content }}
      </h3>
      <button @click="removeTodo(index)" class="btn">Remove Todo</button>
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

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function removeAllTodos() {
      todos.value = [];
    }

    function markAllTodosDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    return {
      todo,
      todos,
      addNewTodo,
      toggleDone,
      removeTodo,
      removeAllTodos,
      markAllTodosDone,
    };
  },
};
</script>

<style>
#app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  max-width: 700px;
  margin: 40px auto;
  text-align: center;
}

.btn {
  display: block;
  margin: 20px auto;
  padding: 10px;
  border: none;
  background: #eee;
  color: #212121;
  width: 170px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
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

ul {
  padding: 0;
}

.todo {
  list-style: none;
}

.todo h3 {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
