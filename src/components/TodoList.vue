<template>
    <div class="todo-container">
      <h1>To-Do List</h1>
      <div class="add-todo">
        <input v-model="newTodo" placeholder="Tukiskan disini" />
        <button @click="addTodo">Tambahkan</button>
      </div>
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <span v-if="!todo.editing">{{ todo.text }}</span>
          <input v-else v-model="todo.text" @keyup.enter="saveTodo(todo)" />
          <button @click="editTodo(todo)">Edit</button>
          <button @click="deleteTodo(index)">Hapus</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newTodo: '',
        todos: [],
      };
    },
    methods: {
      addTodo() {
        if (this.newTodo.trim() !== '') {
          this.todos.push({ text: this.newTodo, editing: false });
          this.newTodo = '';
        }
      },
      editTodo(todo) {
        todo.editing = true;
      },
      saveTodo(todo) {
        todo.editing = false;
      },
      deleteTodo(index) {
        this.todos.splice(index, 1);
      },
    },
  };
  </script>
  
  <style scoped>
  .todo-container {
    background: linear-gradient(to bottom right, pink, purple);
    padding: 20px;
    border-radius: 10px;
    max-width: 400px;
    margin: 0 auto;
    text-align: center;
    color: white;
  }
  .add-todo {
    margin-bottom: 20px;
  }
  input[type='text'] {
    padding: 10px;
    border-radius: 5px;
    border: none;
    width: calc(100% - 60px);
    margin-right: 10px;
  }
  button {
    padding: 10px;
    border-radius: 5px;
    border: none;
    cursor: pointer;
    background-color: #fff;
    color: #000;
  }
  button:hover {
    background-color: #ddd;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 10px 0;
    background: rgba(255, 255, 255, 0.2);
    padding: 10px;
    border-radius: 5px;
  }
  </style>
  