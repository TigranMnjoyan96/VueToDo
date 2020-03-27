<template>
    <li>
        <span :class="{v__done: todo.completed}">
            <input type="checkbox" @change="todo.completed = !todo.completed">
            <strong>{{idx + 1}}</strong>
            {{todo.title}}
        </span>
        <button class="v__delete__btn" @click="deleteItem">&times;</button>
    </li>
</template>

<script>
    export default {
        name: "v-list",
        props: {
            todo: {
                type: Object,
                required: true
            },
            idx: Number
        },
        methods: {
            deleteItem() {
                this.$emit('isDone', this.todo.id)
            }
        }
    }
</script>

<style scoped>
    li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: 1rem;
    }
    .v__delete__btn {
        background: red;
        border: none;
        color: white;
        font-size: 18px;
        border-radius: 3px;
        font-weight: bold;
    }
    input {
        margin-right: .5rem;
    }
    .v__done {
        text-decoration: line-through;
    }
</style>