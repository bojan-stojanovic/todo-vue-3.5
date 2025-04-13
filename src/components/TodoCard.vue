<script setup lang="ts">
defineProps<{
    message: string;
    completed: boolean;
    id: string;
}>();

const emit = defineEmits<{
    removeTodo: [id: string];
    todoStatus: [id: string];
}>();
</script>

<template>
    <div class="todo-card" :class="{ completed: completed }">
        <p>{{ message }}</p>
        <div class="todo-card__controls">
            <button class="toggle" @click="emit('todoStatus', id)">
                Mark as done
            </button>
            <button class="remove" @click="emit('removeTodo', id)">
                Remove
            </button>
        </div>
    </div>
</template>

<style scoped>
.todo-card {
    display: grid;
    grid-template-columns: 1fr auto;
    border: 2px solid #ccc;
    gap: 1rem;
    padding: 1rem;
    transition: all 0.3s;

    &.completed {
        border-color: #00853e;
        background-color: rgba(0, 133, 62, 0.35);
    }

    p {
        margin: 0;
    }
}

.todo-card__controls {
    display: grid;
    gap: 1rem;
}

.remove {
    background-color: #c12727;
    color: #fff;
}

.toggle {
    background-color: #00853e;
    color: #fff;
}
</style>
