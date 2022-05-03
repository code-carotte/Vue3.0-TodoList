<template>
	<div class="input-add">
		<input type="text" v-model="todoContent" @keyup.enter="emitAddTodo" />
		<!-- <button>+</button> -->
		<button @click="emitAddTodo">
			<i class="plus"></i>
		</button>
	</div>
</template>

<script>
import { ref } from 'vue'
export default {
    name: 'TodoAdd',
    props: ['tid'],
    setup(props, { emit }) {
        const todoContent = ref('');

        const emitAddTodo = () => {
            if (!todoContent.value) {
                return
            }
            const todo = {
                id: props.tid,
                content: todoContent.value,
                completed: false,
            };
            emit('add-todo', todo);
            todoContent.value = '';
        }

        return {
            todoContent,
            emitAddTodo
        }
    }
};
</script>

<style>
    .input-add {
        position: relative;
        display: flex;
        align-items: center;
    }
    .input-add input {
        padding: 16px 52px 16px 18px;
        border-radius: 48px;
        border: none;
        outline: none;
        box-shadow: 0px 0px 24px rgba(0, 0, 0, .1);
        width: 100%;
        font-size: 16px;
        color: #626262;
    }
    .input-add button {
        position: absolute;
        right: 0;
        width: 46px;
        height: 46px;
        border-radius: 50%;
        background-image: linear-gradient(120deg, #a1c4fd 0%, #c2e9fb 100%);
        border: none;
        outline: none;
        color: white;
        cursor: pointer;
    }
    .input-add .plus {
        display: block;
        width: 100%;
        height: 100%;
        background-image: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
        background-size: 50% 2px, 2px 50%;
        background-position: center;
        background-repeat: no-repeat;
    }
</style>