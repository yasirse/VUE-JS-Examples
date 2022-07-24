<script>
// give each todo a unique id
  let id = 0
export default {
  data() {
    return {
      count: 0,
       text: '',
        message: 'Hello World!',
      counter:
      {
        count: 0
      },
      titleClass: 'title',
      message: 'Hello World!',
      awesome: true,

      // example of Todolist-----------------------------------------------------------
      hideCompleted: false,
       newTodo: '',
        todos:
        [
        { id: id++, text: 'Learn HTML' },
        { id: id++, text: 'Learn JavaScript' },
        { id: id++, text: 'Learn Vue' }
        ],
     //watcher--------------------------------------------------------
     todoId: 1,
     todoData: null    
    }

  },
   computed:
   {
    filteredTodos()
    {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos
    },
     mounted()
    {
      this.$refs.p.textContent = 'mounted!'
    }
    },
  methods: {
    increment() {
      this.count++
    },
     onInput(e) {
      this.text = e.target.value
    },
    toggle() {
      this.awesome = !this.awesome
    },
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    },
    //watcher--------------------------------------------------------
    async fetchData() 
    {
      this.todoData = null
      const res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${this.todoId}`
      )
      this.todoData = await res.json()
    }
    //end of watcher--------------------------------------------------------
   },
  mounted() {
    this.fetchData()
  },
  watch: {
    todoId() {
      this.fetchData()
    }
  }
}
</script>

<template>

<div class="col-sm-12" id="app1">
  <h1>VUE practice example </h1>
  <p ref="p">hello</p>
</div>
<div class="col-sm-12" id="app1">
   <h1>{{ message }}</h1>
</div>
<div class="col-sm-12" id="app1">
  <p>Count is: {{ counter.count }}</p>
</div>
<div class="col-sm-12" id="app1">
  <div><button @click="increment">count is: {{ count }}</button></div>
</div>
<div class="col-sm-12" id="app1">
   <input :value="text" @input="onInput" placeholder="Type here">
  <p>{{ text }}</p>
</div>
<div class="col-sm-12" id="app1">
   <h1 :class="titleClass">Make me red</h1>
</div>
<div class="col-sm-12" id="app1">
   <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
</div>
<div class="col-sm-12" id="app1">
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</div>
<div class="col-sm-12" id="app1">
  <h5>Second example of todolist</h5>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form> 
  
   <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</div>

<div class="col-sm-12" id="app1">
    <h5>Fetching data from URL using watch command</h5>
  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
</div>
</template>
<style>
.title {
  color: red;
}
.done {
  text-decoration: line-through;
}
</style>`
