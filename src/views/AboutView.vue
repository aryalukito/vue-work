<script>
import { createInterpolation } from '@vue/compiler-core'

let id = 0

export default {
    data() {
        return {
            newTodo: "",
            hideCompleted: false,
            todos: [
                { id: id++, text: "Bangun Pagi", done: true },
                { id: id++, text: "Olahraga", done: true },
                { id: id++, text: "Bersepeda", done: false }
            ]
        };
    },
    computed: {
        filteredTodos() {
            return this.hideCompleted
                ? this.todos.filter((t) => !t.done)
                : this.todos;
        }
    },
    methods: {
        addTodo() {
            this.todos.push({ id: id++, text: this.newTodo, done: false });
            this.newTodo = "";
        },
        removeTodo(todo) {
            this.todos = this.todos.filter((t) => t !== todo);
        }
    },
    components: { createInterpolation }
}
</script>

<template>
  <div class="wrap">
  <div class="container">
  <div class="container-1">
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <center><button>Add List</button></center>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <center><button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button></center>
</div>
</div>
</div>
</template>

<style>
.done {
  text-decoration: line-through;
}
.wrap {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  border: 1px solid rgba(255, 255, 255, .5);
  border-radius: 15px;
  min-width: 300px;
  max-width: 300px;
  min-height: 100px;
}
.container .container-1 {
  margin: 50px;
}

li {
  display: flex;
  justify-content: space-between;
  margin-left: -20%;
}

ul li {
  list-style-type: none;
}

button {
  border-radius: 10px;
}
button:hover {
  background-color: hsla(160, 100%, 37%, 1);
}

form input {
  border-radius: 10px; 
  width: 100%;
}


</style>