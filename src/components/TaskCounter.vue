<template>
  <p>Task count <span class="count">{{ count }} / 10</span></p>
</template>

<script>
export default {
  name: 'TaskCounter',
  props: {
    count: Number,
  }
}
</script>
<style scoped lang="scss">
@import '../styles/variables';
p {
  margin: 0 0 15px;
}

.count {
  margin-left: 5px;
  color: $blue;
  font-weight: bold;
}
</style>
