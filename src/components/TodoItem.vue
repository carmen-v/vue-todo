<script setup>
import { Icon } from '@iconify/vue'
// eslint-disable-next-line no-unused-vars
const props = defineProps({
  todo: {
    type: Object,
    required: true
  },
  index: {
    type: Number,
    required: true
  }
})
</script>
<template>
  <li>
    <input type="checkbox" :checked="todo.completed" @input="$emit('toggle-complete', index)" />
    <div class="todo">
      <input
        v-if="todo.isEditing"
        type="text"
        :value="todo.todo"
        @input="$emit('update-todo', $event.target.value, index)"
      />
      <span
        v-else
        :class="{
          'completed-todo': todo.completed
        }"
      >
        {{ todo.todo }}
      </span>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        icon="ph:check-circle"
        class="icon"
        color="#42b883"
        width="22"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        v-else
        icon="ph:pencil-fill"
        class="icon"
        color="#06768d"
        width="22"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        icon="ph:trash"
        class="icon"
        color="#e0115f"
        width="22"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
  </li>
</template>
<style lang="scss"></style>
