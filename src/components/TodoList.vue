<script setup lang="ts">
import TodoCard from "./TodoCard.vue";

defineProps<{
    filteredTodos: { id: string, message: string; completed: boolean }[];
}>();

const emit = defineEmits<{
    removeTodo: [id: string];
    todoStatus: [id: string];
}>();
</script>

<template>
    <div class="todo-list">
        <TodoCard
            v-for="todo in filteredTodos"
            :message="todo.message"
            :completed="todo.completed"
            :id="todo.id"
            :key="todo.id"
            @remove-todo="emit('removeTodo', todo.id)"
            @todo-status="emit('todoStatus', todo.id)"
        />
    </div>
</template>

<style scoped>
.todo-list {
    display: grid;
    gap: 1rem;
}
</style>
