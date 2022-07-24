<script>
import HelloWorld3 from './HelloWorld3.vue'
export default {
  data() {
    return {
      todoId: 1,
      todoData: null,
      greeting: 'Hello from parent',
      childMsg: 'No child msg yet'
    }
  },
  methods: {
    async fetchData()
    {
      this.todoData = null
      const res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${this.todoId}`
      )
      this.todoData = await res.json()
    }
  },
  mounted() {
    this.fetchData()
  },
  watch: {
    todoId() {
      this.fetchData()
    }
  },
  components: {
    HelloWorld3
  }
}
</script>

<template>
<div class="col-sm-12" id="app1">
  <HelloWorld3 :msg1="greeting" @response="(msg) => childMsg = msg"/>
  <p>{{ childMsg }}</p>
  <h5>Fetching data from URL using watch command from different page and app of VUE</h5>
  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
  </div>
</template>