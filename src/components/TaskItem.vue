<template>
  <div>
    <p>{{ title }}</p>
  </div>
</template>

<script>
export default {
  name: 'TaskItem',
  props: {
    id: Number,
    title: String,
  }
}
</script>
<style scoped>
</style>
