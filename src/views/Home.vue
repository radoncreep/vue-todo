<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <!-- getting the todos data into the Todos component by passing it in w a directive called v-bind -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos';
import Header from '../components/layout/Header';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data () {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) { // we are deleting here bcos this is where we have array of objects
      // let todosData = [...this.todos];

      // // filter object w equal id
      // todosData = todosData.filter(todoItem => todoItem.id !== id);
      // this.todos = todosData;

      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => {
            this.todos = res.data.filter(todoItem => todoItem.id !== id);
        })
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      }).then(res => {
        this.todos = [...this.todos, res.data]
      }).catch(err => console.log(err));
      this.todos = [...this.todos, newTodo];
    }
  },
  created () { // works like componentDidMount() i.e it fires off when the component loads
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => {
        this.todos = response.data;
        console.log(this.todos)
      })
      .catch(error => console.log(error))
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: lightgrey;
  }
</style>
