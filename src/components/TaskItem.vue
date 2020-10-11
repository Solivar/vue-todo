<template>
  <div>
    <p>{{ title }}</p>
    <button @click="deleteTask">X</button>
  </div>
</template>

<script>
export default {
  name: 'TaskItem',
  props: {
    id: Number,
    title: String,
  },
  methods: {
    deleteTask: function() {
      this.$emit('deleteTask', this.id);
    }
  }
}
</script>
<style scoped>
</style>
