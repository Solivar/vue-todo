<template>
  <div class="task">
    <div class="completion">
      <input type="checkbox"
        @change="toggleCompletion"
        v-model="isCompleted"
      >
    </div>
    <p
      class="title"
      v-bind:class="{ striked: isCompleted }"
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
@import '../styles/variables';

.task {
  display: flex;
  justify-content: space-between;
  margin-bottom: 15px;
  background-color: #ffffff;
  border: 1px solid $grey;
  border-radius: 5px;
  padding: 10px;
}

.title {
  cursor: pointer;
}

.striked {
  text-decoration: line-through;
}

p {
  margin: 0;
  width: calc(100% - 64px);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.completion {
  padding: 0 10px 0 0;
  margin: -10px 0 -10px;
  border-right: 1px solid $grey;
  display: flex;
  align-items: center;

  input {
    margin: 0;
  }
}

button {
  border: none;
  border-left: 1px solid $grey;
  color: $blue;
  background: none;
  padding: 0 10px;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin: -10px -10px -10px 0;
  font-weight: bold;
  cursor: pointer;

  &:hover, &:active {
    color: $red;
  }
}
</style>
