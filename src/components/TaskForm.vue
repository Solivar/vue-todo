<template>
  <form @submit.prevent="onSubmit">
    <p>{{ title }}</p>
    <input type="text" v-model="title">
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  name: 'TaskForm',
  data: () => {
    return {
      title: '',
      errors: [],
    }
  },
  methods: {
    onSubmit: function () {
      this.errors = [];

      if (this.title.length < 2) {
        this.errors.push('Task title is required');
      }

      this.$emit('addTask', this.title);

      this.title = '';
    }
  }
}
</script>
<style scoped>
</style>
