<template>
    <ul>
        <v-list v-for="(item, idx) in todos" :key="item.id" :idx="idx" :todo="item" @isDone="isDone"></v-list>
    </ul>
</template>

<script>
    import vList from './list/v-list';
    export default {
        name: "v-todo-list",
        props: {
            todos: {
                type: Array,
                default: []
            }
        },
        components: {
            vList
        },
        methods: {
            isDone(id) {
                this.$emit('isDone', id)
            }
        }
    }
</script>

<style scoped>
    ul {
        list-style: none;
        width: 40%;
        margin: 50px auto 0;
    }
</style>