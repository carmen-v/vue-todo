<script setup>
import { Icon } from '@iconify/vue';
// eslint-disable-next-line no-unused-vars
const props = defineProps({
    todo: {
        type: Object,
        required: true,
    },
    index: {
        type: Number,
        required: true
    }
})
defineEmits(['toggle-complete', 'edit-todo', 'update-todo', 'delete-todo']);

</script>
<template>
    <li>
        <input type="checkbox" :checked="todo.isCompleted" @input="$emit('toggle-complete', index)" />
        <div class="todo">
            <input v-if="todo.isEditing" type="text" :value="todo.todo" @input="$emit('update-todo', $event.target.value, index)"/>
            <span
        v-else
        :class="{
          'completed-todo': todo.isCompleted,
        }"
      >
        {{ todo.todo }}
      </span>
        </div>
        <div class="todo-actions">
            <Icon v-if="todo.isEditing" icon="ph:check-circle" class="icon" color="#42b883" width="22" @click="$emit('edit-todo', index)"/>
            <Icon v-else icon="ph:pencil-fill" class="icon" color="#2cbad3" width="22" @click="$emit('edit-todo', index)"/>
            <Icon icon="ph:trash" class="icon" color="#E0115F" width="22" @click="$emit('delete-todo', todo.id)"/>
        </div>
    </li>
</template>
