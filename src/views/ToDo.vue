<script setup>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'

const todoList = ref([
  { id: uuidv4(), text: "Swim" },
  { id: uuidv4(), text: "Smoke" },
  { id: uuidv4(), text: "Stretch" },
  { id: uuidv4(), text: "Check" }
])

const text = ref('')

const onInput = (e) => {
  text.value = e.target.value
}

const addTodo = () => {
  if (text.value.trim() == '') {
    alert('Please write something')  
  } 
  else {
    todoList.value.push({
    id: uuidv4(), text: text.value
  });
  }
  text.value=''
  
}

const deleteTodo = (todo) => {
  todoList.value = todoList.value.filter(task => task != todo)
}

</script>

<template>
  <div class="todolist">
    <h1>To-Do List with Vue</h1>
    <div class="input-group mb-3">
      <input v-model="text" class="form-control" placeholder="New task to do" aria-label="New task to do"
        aria-describedby="basic-addon2" @keydown.enter="addTodo">
      <div class="input-group-append">
        <button class="btn btn-outline-success" type="button" @click="addTodo">Add task</button>
      </div>
    </div>
    <div>
      <ul>
        <li v-for="todo in todoList" v-bind:key="todo.id" class="todo-item">
          {{ todo.text }}
          <button type="button" class="btn btn-outline-success delete-btn" @click="deleteTodo(todo)">Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .todo-list {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }

  .todo-item {
    position: relative;
    margin-bottom: 10px;
  }

  .delete-btn {
    position: absolute;
    right: 0;
    top: 0;
    display: none;
    font-size: 0.8rem;
  }

  .todo-item:hover .delete-btn {
    display: inline-block;
  }
}
</style>
