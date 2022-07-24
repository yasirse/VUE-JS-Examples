<script>

export default 
{
  data() {
    return {
      todoIdr: 1,
      todoDatar: null
    }
  },
  props:
  {
    msg1: String
  },
  emits: ['response'],
  created()
  {
    this.$emit('response', 'Hello from child ooooo')
  }
}
</script>

<template>
<p>{{ msg1 }}</p>
</template>