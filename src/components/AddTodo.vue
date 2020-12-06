<template>
    <div>
        <!-- we have to traverse to the root where the data lies -->
        <!-- the reason for not adding $emit is to construct the todo data and then send it and emit it in the event -->
        <form @submit="addTodo">
            <input v-model="title" type="text" name="title" placeholder="Add Todo..">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
// import { v4 as uuidv4 } from 'uuid';

export default {
    name: 'AddTodo',
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault(); // prevents the form from submitting to a file
            const newTodo = {
                // id: uuidv4(),
                title: this.title,
                completed: false
            }
            console.log(newTodo.id)

            // send up to parent
            this.$emit('add-todo', newTodo);

            this.title = "";
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2;
    }

</style>