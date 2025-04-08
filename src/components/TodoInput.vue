<script setup lang="ts">
import { ref } from "vue";

// emmiters
const emit = defineEmits<{
    addTodo: [todo: string];
}>();

const inputValue = ref("");
const isEmpty = ref(false);

function submitTodoHandler() {
    if (inputValue.value.trim() === "") {
        isEmpty.value = true;

        const timeOut = setTimeout(() => {
            isEmpty.value = false;

            clearInterval(timeOut);
        }, 2000);

        return;
    }

    emit("addTodo", inputValue.value);

    inputValue.value = "";
}
</script>

<template>
    <form class="form" @submit.prevent="submitTodoHandler">
        <div>
            <label for="todoInput"></label>
            <input
                type="text"
                id="todoInput"
                name="todoInput"
                placeholder="Add your todo"
                class="input"
                v-model="inputValue"
            />
            <p class="error" v-if="isEmpty">Please add todo</p>
        </div>

        <button class="button">Add</button>
    </form>
</template>

<style scoped>
.form {
    display: grid;
    gap: 1rem;

    > div {
        display: grid;
        gap: 0.5rem;
    }
}

.input {
    width: 100%;
    padding: var(--element-padding);
}

.button {
    justify-self: end;
    background-color: #0040ff;
    color: #fff;
}

.error {
    color: red;
    font-size: 0.85rem;
}
</style>
