<template>
  <p>{{ count }} / 10</p>
</template>

<script>
export default {
  name: 'TaskCounter',
  props: {
    count: Number,
  }
}
</script>
<style scoped>
</style>
