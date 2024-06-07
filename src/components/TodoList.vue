<template>
  <div class="todo-app">
    <h1>Todo List</h1>
    <div class="input-group">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new todo" />
      <button @click="addTodo">Add</button>
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todoStore.todos" :key="index" :class="{ completed: todo.completed }">
        <div class="todo-item">
          <input type="checkbox" v-model="todo.completed" />
          <span>{{ todo.text }}</span>
        </div>
        <button @click="removeTodo(index)" class="delete-button">Delete</button>
      </li>
    </ul>
    <p class="incomplete-tasks">Incomplete tasks: {{ todoStore.incompleteTodos }}</p>
  </div>
</template>

<script>
import { ref } from 'vue'
import { useTodoStore } from '../stores/todoStore'

export default {
  name: 'TodoList',
  setup() {
    const todoStore = useTodoStore()
    const newTodo = ref('')

    const addTodo = () => {
      if (newTodo.value.trim()) {
        todoStore.addTodo(newTodo.value.trim())
        newTodo.value = ''
      }
    }

    const removeTodo = (index) => {
      todoStore.removeTodo(index)
    }

    return {
      todoStore,
      newTodo,
      addTodo,
      removeTodo,
    }
  }
}
</script>

<style scoped>
.todo-app {
  max-width: 1000px;
  margin: 1rem auto;
  padding: 5rem;
  background: #786767;
  box-shadow: 0 0 15px rgba(255, 252, 252, 0.1);
  border-radius: 30px;
  text-align: center;
  font-family: Arial, sans-serif;
  justify-content: center;
  margin: 250px;
}


h1 {
  margin-bottom: 2rem;
  color: #333;
  font-size: 2.5rem;
}

.input-group {
  display: flex;
  justify-content: center;
  margin-bottom: 2rem;
}

.input-group input {
  padding: 1rem;
  font-size: 1.25rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  flex: 1;
  margin-right: 0.5rem;
}

.input-group button {
  padding: 1rem 2rem;
  font-size: 1.25rem;
  background-color: #19a90f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.input-group button:hover {
  background-color: #054cf1;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  border-bottom: 1px solid #ffffff;
}

.todo-list li:last-child {
  border-bottom: none;
}

.todo-item {
  display: flex;
  align-items: center;
}

.todo-item input[type="checkbox"] {
  margin-right: 1rem;
  transform: scale(1.5);
}

.todo-list li.completed span {
  text-decoration: line-through;
  color: grey;
}

.delete-button {
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
  font-size: 1.25rem;
}

.delete-button:hover {
  background-color: #c82333;
}

.incomplete-tasks {
  margin-top: 2rem;
  font-weight: bold;
  color: #333;
  font-size: 1.5rem;
}
</style>
