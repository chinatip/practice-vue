<template>
  <div id="app">
  <inputBox @save="saveTodo"></inputBox>
  <todoList :todos="todos" @update="updateTodo"></todoList>
  </div>
</template>

<script>

import lodash from 'lodash';
import todoList from './todoList';
import inputBox from './inputBox';

export default {
  name: 'app',
  components: { todoList, inputBox },
  data() {
    return {
      text: 'Hello',
      newTodo: '',
      todos: [
        {
          text: 'Learn Vue.js',
          completed: true,
          time: 15685692784,
        }, {
          text: 'Learn VueX',
          completed: false,
          time: 15515451954,
        }, {
          text: 'Learn Vue Router',
          completed: false,
          time: 15685241856,
        }
      ]
    }
  },
  mounted () {
    this.todos = JSON.parse(localStorage['todos'] || '[]');
  },
  methods: {
    saveTodo(todo) {
      this.todos.push({
        text: todo,
        time: Date.now().toString(),
        completed: false,
      });

      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    updateTodo(time, type) {
      let newTodos = this.todos;

      if (type === 'remove') {
        newTodos = lodash.filter(newTodos, (t) => t.time !== time);
      } else {
        newTodos.forEach((t) => {
          if (t.time === time && type === 'status') {
            t.completed = !t.completed;
          }
        });
      }

      this.todos = newTodos;
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
  }
}
</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin: auto;
    max-width: 700px;
    margin-top: 60px;
  }
</style>
