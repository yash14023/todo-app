<template>
    <div class="p-4">
      <h1 class="text-center text-2xl font-bold mb-4">Todo List</h1>
      <form @submit.prevent="add" class="mb-6 flex justify-center">
        <input v-model="newTodo" class="border rounded p-2 mr-2 text-black">
        <button class="bg-blue-500 hover:bg-blue-700 text-black font-bold py-2 px-4 rounded">
          +
        </button>
      </form>
      <ul>
        <li v-for="todo in todos" :key="todo.id" class="flex items-center mb-2 p-2 bg-white shadow-md rounded">
          <span class="mr-2 text-lg text-black text-[22px]">{{ todo.text }}</span>
          <h11 class="text-sm text-gray-400">{{ formattedDatetime(todo.createdAt) }}</h11>
          <button @click="remove(todo)" class="bg-red-500 hover:bg-red-700 text-white font-bold py-1 px-2 rounded">
            -
          </button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      let id = 0;
      const newTodo = ref('');
      const todos = ref([
        { id: id++, text: 'assignment on TODO', createdAt: new Date() }
      ]);
  
      const formattedDatetime = (datetime) => {
        const options = { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' };
        return datetime.toLocaleDateString(undefined, options).toLowerCase();
      };
  
      function add() {
        todos.value.push({ id: id++, text: newTodo.value, createdAt: new Date() });
        newTodo.value = '';
      }
  
      function remove(todo) {
        const index = todos.value.indexOf(todo);
        if (index !== -1) {
          todos.value.splice(index, 1);
        }
      }
  
      return { newTodo, todos, formattedDatetime, add, remove };
    }
  }
  </script>
  