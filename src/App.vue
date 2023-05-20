<template>
    <div class="container">
        <h2>TO-DO List</h2>

        <form @submit.prevent="onSubmitTodo">
            <div class="d-flex">
                <div class="flex-grow-1 mr-2">
                    <input class="form-control" type="text" v-model="inputTodo" placeholder="Type new to-do"/>
                </div>

                <div>
                    <button class="btn btn-primary" type="submit">Add</button>
                </div>
            </div>
            <div v-if="hasError" class="has-error">할 일 목록을 입력해 주세요.</div>
        </form>
        <div class="card mt-2" :key="todo.id" v-for="(todo, index) in todos">
            <div class="card-body p-2 d-flex align-items-center">
                <div class="form-check flex-grow-1">
                    <input v-model="todo.completed" class="form-check-input" type="checkbox">
                    <label class="form-check-label" :class="{todo: todo.completed}">{{ todo.subject }}</label>
                </div>
                <div>
                    <button class="btn btn-danger btn-sm" @click="onClickDeleteTodo(index)">Delete</button>
                </div>
            </div>
        </div>
        <div v-if="todos.length === 0">추가된 todo 가 없습니다.</div>
    </div>
</template>

<script>
import {ref} from 'vue';

export default {
    setup() {
        const todos = ref([]);
        const inputTodo = ref('');
        const hasError = ref(false);
        const todoStyled = {
            textDecoration: 'line-through',
            color: 'gray'
        }

        const onSubmitTodo = () => {
            if (inputTodo.value === '') {
                hasError.value = true;
            } else {
                todos.value.push({
                    id: Date.now(),
                    subject: inputTodo.value,
                    completed: false
                });
                inputTodo.value = '';
                hasError.value = false;
            }
        }

        const onClickDeleteTodo = (index) => {
            console.log(index)
            todos.value.splice(index, 1);
        }

        return {todos, inputTodo, hasError, todoStyled, onSubmitTodo, onClickDeleteTodo};
    }
}

</script>

<style>
.has-error {
    color: tomato;
}

.todo {
    color: gray;
    text-decoration: line-through;
}
</style>