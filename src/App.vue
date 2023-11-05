<script setup>
import { RouterView } from 'vue-router'
import TodosHeader from './components/TodosHeader.vue';

</script>

<template>
  <TodosHeader />
  <RouterView />
</template>
<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&family=Nunito&family=Sora&display=swap');
* {
    font-family: "Rubik", sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
</style>