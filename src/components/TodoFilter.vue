<script setup lang="ts">
defineProps<{
    todoNumber: number;
    activeFilter: string;
}>();

const emit = defineEmits<{
    updateActiveFilter: [filter: string];
}>();
</script>

<template>
    <div class="filter-wrapper">
        <span>Number of todos: {{ todoNumber }}</span>
        <div class="filters">
            <button
                :class="{ active: activeFilter === 'all' }"
                @click="emit('updateActiveFilter', 'all')"
            >
                All
            </button>
            <button
                :class="{ active: activeFilter === 'done' }"
                @click="emit('updateActiveFilter', 'done')"
            >
                Done
            </button>
            <button
                :class="{ active: activeFilter === 'open' }"
                @click="emit('updateActiveFilter', 'open')"
            >
                Open
            </button>
            <span>Active filter {{ activeFilter }}</span>
        </div>
    </div>
</template>

<style scoped>
.filter-wrapper {
    display: flex;
    justify-content: space-between;
}

.filters {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: flex-end;

    button {
        transition: all 0.3s;

        &:hover {
            background-color: #537eff;
            color: #fff;
        }

        &.active {
            background-color: #0040ff;
            color: #fff;
        }
    }

    span {
        flex: 1 0 100%;
        text-align: right;
    }
}
</style>
