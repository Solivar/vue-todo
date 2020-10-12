<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title">
    <button type="submit">Add</button>
    <p class="error" v-show="error">{{ error }}</p>
  </form>
</template>

<script>
export default {
  name: 'TaskForm',
  props: {
    count: Number,
  },
  data: () => {
    return {
      title: '',
      error: '',
    }
  },
  methods: {
    onSubmit: function () {
      this.error = '';

      if (this.count === 10) {
        this.error = 'Task limit reached';

        return;
      }

      if (this.title.length < 2 || this.title.length > 50) {
        this.error = 'Task title is must be 2-50 characters long';

        return;
      }

      this.$emit('addTask', this.title);

      this.title = '';
    }
  }
}
</script>
<style scoped lang="scss">
@import '../styles/variables';

form {
  margin-bottom: 30px;
}

input {
  border: 1px solid $grey;
  padding: 2px 15px;
  height: 25px;
  box-sizing: border-box;
  border-radius: 5px;
  margin-right: 5px;
}

button {
  background: $green;
  color: #ffffff;
  border: 0;
  height: 25px;
  width: 80px;
  padding: 0;
  border-radius: 10px;
  font-weight: bold;
  text-transform: uppercase;

  &:hover, &:active {
    background: darken($color: $green, $amount: 5%);
    cursor: pointer;
  }
}

.error {
  color: $red;
  margin: 10px 0 0;
}
</style>
