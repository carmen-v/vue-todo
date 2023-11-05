<script setup>
import { ref, watch } from 'vue'
import { uid } from 'uid'
import TodoForm from '../components/TodoForm.vue'
import TodoItem from '../components/TodoItem.vue'
import { Icon } from '@iconify/vue'
const todoList = ref([])

watch(
  todoList,
  () => {
    setTodoListLocalStorage()
  },
  {
    deep: true
  }
)

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem('todoList'))
  if (savedTodoList) {
    todoList.value = savedTodoList
  }
}

fetchTodoList()
const actualFetchTodoList = () => {
  //get all available todos from API:
  fetch('https://dummyjson.com/todos')
      .then(response => response.json())
      .then(data => todoList.value = data.todos);
}

actualFetchTodoList()

const setTodoListLocalStorage = () => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value))
}

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null
  })
}

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
}

const toggleEditTodo = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing
}

const updateTodo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal
}

const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId)
}
</script>

<template>
    <h1>You can do it!</h1>
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem
        :key="todo.id"
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:exclamation-mark" color="#2cbad3" width="22" />
      <span>You have no to-dos to complete. Add one. </span>
    </p>
    <TodoForm @create-todo="createTodo" />
</template>

<style lang="scss" scoped>
.todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
</style>