<script>
export default {
  data() {
    return {
      message: 'Hello World!',
      counter:
      {
        count: 0
      },
      titleClass: 'title'
    }
    
  }
}
</script>

<template>
  <h1>{{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
   <h1 :class="titleClass">Make me red</h1>
</template>

<style>
.title {
  color: red;
}
</style>