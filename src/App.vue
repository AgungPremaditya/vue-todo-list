<script lang="ts">
import Header from "./components/Header.vue";
import { ref, defineComponent } from "vue";

export default defineComponent({
  components: { Header },
  setup() {
    const newTodo = ref("");
    const STORAGE_KEY = "todos";

    const defaultData = [
      {
        done: false,
        content: "Trying todo Something",
      },
    ];
    localStorage.setItem(STORAGE_KEY, JSON.stringify(defaultData));

    const todosData = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
    const todos = ref(todosData);

    function addTodo() {
      if (newTodo.value) {
        todos.value.push({
          done: false,
          content: newTodo.value,
        });
        newTodo.value = "";
      }
      saveData();
    }

    function doneTodo(todo: { done: boolean }) {
      todo.done = !todo.done;
      saveData();
    }

    function removeTodo(index: number) {
      todos.value.splice(index, 1);
      saveData();
    }

    function saveData() {
      const storageData = JSON.stringify(todos.value);
      localStorage.setItem("todos", storageData);
    }

    return {
      todos,
      newTodo,
      addTodo,
      doneTodo,
      removeTodo,
    };
  },
});
</script>

<template>
  <Header />
  <div class="container">
    <form class="form-wrapper" @submit.prevent="addTodo()">
      <label>New ToDo</label>
      <input type="text" name="newTodo" v-model="newTodo" class="form-input" />
      <button class="button">Add ToDo</button>
    </form>
    <div class="list-wrapper">
      <h4>ToDo List</h4>
      <ul class="todo-list">
        <li v-for="(todo, index) in todos">
          <span :class="{ done: todo.done }" @click="doneTodo(todo)">{{
            todo.content
          }}</span>
          <button class="remove-btn" @click="removeTodo(index)">Remove</button>
        </li>
        <li v-if="todos.length === 0" class="empty">
          <span>EMPTY LIST</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.list-wrapper {
  width: 50%;
}
.list-wrapper h4 {
  padding: 0;
  margin: 0;
  color: white;
}
.todo-list {
  color: white;
  list-style-type: none;
  padding: 0;
  margin: 0;
}
.todo-list li {
  display: flex;
  margin: 0.5em 0 1em 0;
  padding: 1em;
  border: 3px rgba(255, 255, 255, 0.247) solid;
  border-radius: 0.8em;
  align-items: center;
}
.todo-list li span {
  width: 80%;
}
.todo-list .done {
  text-decoration: line-through;
  opacity: 0.7;
}
.todo-list .empty {
  border: none;
}
.remove-btn {
  background: #ff3968;
  color: white;
  border: 0;
  outline: 0;
  padding: 0.3em 0.6em;
  border-radius: 0.6em;
}
</style>
