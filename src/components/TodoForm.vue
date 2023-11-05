<script setup>
import { reactive, defineEmits } from 'vue';

const emit = defineEmits(['create-todo']);

const todoState= reactive({
    todo: "",
    invalid: null,
    errMsg: "",
})

const createTodo = () => {
    todoState.invalid = null;
    if (todoState.todo !== "") {
emit('create-todo', todoState.todo);
todoState.todo = ""; 
return
}
todoState.invalid = true;
todoState.errMsg = "Todo value cannot be empty"
};

</script>

<template>
    <div class="input-wrap" :class="{'input-err' : todoState.invalid}">
        <input type="text" v-model="todoState.todo"/>
        <button @click="createTodo()">Submit</button>
       
    </div>

    <!-- show an error message when there is no text for the todo --> 
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
</template>