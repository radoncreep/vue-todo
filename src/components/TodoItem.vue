<template>
    <!-- we are binding a class on a condition of the "completed" property being true -->
    <!-- if it's value is true then the "is-completed" class will be added to the class -->
    <!-- kind of like class="todo-item is-complete" -->
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <!-- v-on directive is used to add event -->
            <!-- the change event is firing off 123 -->
            <input type="checkbox" v-on:change="markComplete">
            {{ todo.title }}
        </p>
        <!-- we want to emit an event -- we can use v-on:click or @click -->
        <!-- del-todo is the name of the event and the 2nd arg is a parameter we are sending -->
        <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods: { // object of methods
        markComplete() {
            // we want to change value of the completed property of the todo whenever this event is fired off

            // we have to access the todo prop with the this keyword and assign it to a new variable...
            // to avoid props mutation
            let todoProps = this.todo;
            todoProps.completed = !todoProps.completed;
            console.log(todoProps.completed)

            // because of mutation we cant to do this
            // this.todo.completed = !this.todo.completed;
        }
    }
}
</script>

<style scoped>
    .todo-item {
        background: #f4f4f4;
        padding: 15px;
        border-bottom: 1px #ccc dotted;
    }

    .is-complete {
        text-decoration: line-through;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
    
    p {
        display: inline-block;
    }
</style>