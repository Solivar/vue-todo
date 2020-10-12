<template>
  <div class="task">
    <p
      class="title"
      v-bind:class="{ striked: isCompleted }"
      @click="toggleCompletion"
    >
      {{ title }}
    </p>
    <button @click="deleteTask">X</button>
  </div>
</template>

<script>
export default {
  name: 'TaskItem',
  props: {
    id: Number,
    title: String,
    isCompleted: Boolean,
  },
  methods: {
    deleteTask: function() {
      this.$emit('deleteTask', this.id);
    },
    toggleCompletion: function() {
      this.$emit('toggleCompletion', this.id);
    }
  }
}
</script>
<style scoped lang="scss">

.task {
  display: flex;
  margin-bottom: 15px;
}

.title {
  cursor: pointer;
}

.striked {
  text-decoration: line-through;
}

p {
  margin: 0;
}

button {
  border: 0;
  background: none;
  padding: 0;
  margin: 0 0 0 10px;
  font-weight: bold;
  cursor: pointer;
}
</style>
