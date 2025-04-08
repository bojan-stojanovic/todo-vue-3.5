<script setup lang="ts">
import { computed, onMounted, ref } from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoFilter from "./components/TodoFilter.vue";
import TodoList from "./components/TodoList.vue";

type Todo = {
    message: string;
    completed: boolean;
};

const todos = ref<Todo[]>([]);
const activeFilter = ref("all");
const filteredTodos = computed(() => {
    if (activeFilter.value === "done")
        return todos.value.filter((todo) => todo.completed === true);
    if (activeFilter.value === "open")
        return todos.value.filter((todo) => todo.completed === false);
    return todos.value;
});

async function fetchTodos() {
    try {
        const response = await fetch("/json-todos.json");
        const data = await response.json();

        todos.value = [...data];
    } catch (e) {
        console.error(e);
    }
}

function onAddTodo(message: string) {
    const todo = {
        message,
        completed: false,
    };

    todos.value = [todo, ...todos.value];
}

function onFilterTodos(filter: string) {
    if (activeFilter.value === filter) return;

    activeFilter.value = filter;
}

function onRemoveTodo(index: number) {
    todos.value = todos.value.filter((_, i) => i !== index);
}

function onTodoStatus(index: number) {
    todos.value[index].completed = !todos.value[index].completed;
}

onMounted(fetchTodos);
</script>

<template>
    <div class="container">
        <h1>Todo app</h1>
        <TodoInput @add-todo="onAddTodo" />

        <template v-if="todos.length > 0">
            <TodoFilter
                :todo-number="filteredTodos.length"
                :active-filter
                @update-active-filter="onFilterTodos"
            />
            <TodoList
                :filtered-todos
                @remove-todo="onRemoveTodo"
                @todo-status="onTodoStatus"
            />
        </template>
        <p v-else>You don't have any todos yet....</p>
    </div>
</template>

<style scoped>
.container {
    max-width: 70rem;
    margin: 0 auto;
    padding: 0 1rem;
    display: grid;
    gap: 2rem;

    h1 {
        margin: 0;
        text-align: center;
    }
}
</style>
