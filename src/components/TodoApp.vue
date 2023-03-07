<template>
    <div class="todo">
        <form class="todo-form" @submit.prevent="handleSubmit">
            <input class="input" type="text" v-model.trim="input">
            <button class="btn" @click="handleSubmit">Add</button>
        </form>

        <ul class="todo-list">
            <todo-item v-for="todo in todos" :key="todo.id" :todo="todo" :saveTodo="saveTodo" :deleteTodo="deleteTodo" />
        </ul>
    </div>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue'
import TodoItem from '../components/TodoItem.vue'
import type { ITodo } from '../types/index'

export default defineComponent({
    name: "todo-app",
    components: { TodoItem },
    setup() {
        const input = ref('');
        //@ts-ignore
        const data = JSON.parse(localStorage.getItem('todos'));

        const todos = ref<ITodo[]>(data || []);



        const handleSubmit = () => {
            if (input.value === '') return;

            let newTodo = {
                id: Date.now().toString(36),
                text: input.value,
                completed: false
            }

            todos.value.push(newTodo)
            input.value = ''
            saveTodo()
        }

        const saveTodo = () => {
            localStorage.setItem('todos', JSON.stringify(todos.value))
        }

        const deleteTodo = (id: string) => {
            todos.value = todos.value.filter(todo => todo.id !== id)
            saveTodo()
        }

        return {
            input,
            todos,
            handleSubmit,
            saveTodo,
            deleteTodo
        }
    }

})

</script>
<style lang="scss">
.todo {
    max-width: 599px;
    margin: auto;
    display: flex;
    flex-direction: column;

    .todo-form {
        display: flex;
        align-items: stretch;
        justify-content: center;

        .input {
            font-size: 24px;
            padding-left: 10px;
        }

        .btn {
            padding: 0 15px;
            margin-left: 8px;
        }
    }

    .todo-list {
        max-height: 500px;
        overflow-y: auto;
    }
}

form {
    margin: 15px 0;
}
</style>