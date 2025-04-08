<script setup lang="ts">
import TodoCard from "./TodoCard.vue";

defineProps<{
    filteredTodos: { message: string; completed: boolean }[];
}>();

const emit = defineEmits<{
    removeTodo: [index: number];
    todoStatus: [index: number];
}>();
</script>

<template>
    <div class="todo-list">
        <TodoCard
            v-for="(todo, index) in filteredTodos"
            :message="todo.message"
            :completed="todo.completed"
            :index
            :key="index"
            @remove-todo="emit('removeTodo', index)"
            @todo-status="emit('todoStatus', index)"
        />
    </div>
</template>

<style scoped>
.todo-list {
    display: grid;
    gap: 1rem;
}
</style>
