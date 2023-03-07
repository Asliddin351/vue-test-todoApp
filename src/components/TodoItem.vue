<template>
    <li class="todo-item">
        <input class="input" type="checkbox" :checked="todo.completed" @change="handleCompleted(todo)">
        <p class="text" :class="{'checked': todo.completed}">{{ todo.text }}</p>
        <button @click="deleteTodo(todo.id)">❌</button>
    </li>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import type { ITodo } from '../types/index';

interface IProps {
    todo: ITodo,
    saveTodo: () => void,
    deleteTodo: (id: string) => void
}

export default defineComponent({
    name: 'todo-item',
    props: ['todo', 'saveTodo', 'deleteTodo'],
    setup(props) {
        const {todo, saveTodo, deleteTodo} = props as IProps

        const handleCompleted = (todo: ITodo) => {
            todo.completed = !todo.completed
            saveTodo()
        }

        return {
            todo,
            handleCompleted,
            deleteTodo
        }
    }
})
</script>


<style lang="scss" scoped>
    .todo-item {
        border-bottom: 1px solid #000;
        padding: 25px;
        margin-bottom: 8px;
        display: flex;
        justify-content: space-between;
        align-items: stretch;
        background-color: white;
        .text {
            flex: 1;
            padding: 0 15px;
            font-size: 24px;
        }
    }

    .checked {
        text-decoration: line-through;
        color: green;
    }
</style>