<template>
    <main>
        <div class="container">
            <h1>todo-app</h1>
            <todo-add @add-todo="addTodo" :tid="todos.length" />
            <todo-filter :selected="filter" @change-filter="filter = $event" />
            <todo-list :todos="filteredTodos" />
        </div>
    </main>
</template>

<script>
import { ref, computed } from 'vue'
import TodoAdd from './components/TodoAdd.vue'
import TodoFilter from './components/TodoFilter.vue'
import TodoList from './components/TodoList.vue'
export default {
    name: 'App',
    components: {
        TodoAdd,
        TodoFilter,
        TodoList
    },
    setup() {
        const todos = ref([]);
        const addTodo = (todo) => todos.value.push(todo);

        const filter = ref('all');
        const filteredTodos = computed(() => {
            switch (filter.value) {
                case 'done':
                    return todos.value.filter((todo) => todo.completed)
                case 'todo':
                    return todos.value.filter((todo) => !todo.completed)
                default: 
                    return todos.value
            }
        })

        return {
            todos,
            addTodo,
            filter,
            filteredTodos
        }
    }
}
</script>

<style>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
        font-family: Helvetica, 'Mircrosoft Yahei' sans-serif;
    }
    main {
        width: 100vw;
        /* 设置min-height: 这样子页面被容器撑开有滚动条的话，容器的高度也会随之到最底部 */
        min-height: 100vh; 
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgb(179, 217, 252);
    }
    .container {
        width: 60%;
        max-width: 400px;
        box-shadow: 0px 0px 24px rgba(0, 0, 0, .2);
        border-radius: 24px;
        padding: 48px 28px;
        background-color: #f4f6fa;
    }
    h1 {
        margin: 24px 0;
        font-size: 36px;
        color: #626262;
        text-align: center;
    }
</style>
