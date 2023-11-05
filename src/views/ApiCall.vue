
<script setup>
import { ref } from 'vue';
import TodoItem from '../components/TodoItem.vue'
const todoList = ref(null);
const newlyAddedTodos = ref([]); 


//get all available todos from API:
fetch('https://dummyjson.com/todos')
    .then(response => response.json())
    .then(data => todoList.value = data.todos);

  

const addTodo = () => {
  function randomIntFromInterval(min, max) { // get a random todo to add 
  return Math.floor(Math.random() * (max - min + 1) + min)
}

const randomTodo = randomIntFromInterval(0, todoList.value.length);
  newlyAddedTodos.value.push(todoList.value[randomTodo])
};

const toggleTodoComplete = (todoPos) => {
  newlyAddedTodos.value[todoPos].isCompleted = !newlyAddedTodos.value[todoPos].isCompleted
}

const toggleEditTodo = (todoPos) => {
  newlyAddedTodos.value[todoPos].isEditing = !newlyAddedTodos.value[todoPos].isEditing
}

const updateTodo = (todoVal, todoPos) => {
  newlyAddedTodos.value[todoPos].todo = todoVal
}

const deleteTodo = (todoId) => {
  newlyAddedTodos.value = newlyAddedTodos.value.filter((todo) => todo.id !== todoId)
}


</script>

<template>
    <div >
        <button class="add-button" @click="addTodo()">Add a random todo from list</button>
        <ul class="todo-list">
      <TodoItem
        :key="todo.id"
        v-for="(todo, index) in newlyAddedTodos"
        :todo="todo"
        :index="index"
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    </div>
</template>



