<template>
    <form @submit.prevent="addTodo">
        <input type="text" v-model="todo">
        <button type="submit">Create ToDo</button>
    </form>
</template>

<script>
    export default {
        name: "v-add-todo",
        data() {
            return {
                todo: ''
            }
        },
        methods: {
            addTodo() {
                const list = {
                    id: Date.now(),
                    title: this.todo,
                    completed: false
                }
                this.$emit('createTodo', list)
                this.todo = ''
            }
        }
    }
</script>

<style scoped>
    form {
        width: 40%;
        margin: 0 auto;
    }
    input {
        width: 50%;
    }
    button {
        width: 20%;
    }
</style>