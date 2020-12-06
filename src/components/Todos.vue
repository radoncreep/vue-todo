<template>
    <div>
        <!-- since we receive todos data which is an array of object through props.. -->
        <!-- we should loop through the data to get each object using the template directive v-for -->
        <!-- todo can be named anything but "todos" refers to the props we passed in -->
        <!-- todo in todos meaning todo is representing each item/obj in the todos array -->
        <!-- you need a unique key for each item --- using the v-bind:key -->
        <div v-bind:key="todo.id" v-for="todo in todos">
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
        </div>
        <h1>Todos</h1>
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue'
export default {
    name: 'Todos',
    components: {
        TodoItem
    },
    props: ["todos"], 
}
</script>

<style scoped>

</style>