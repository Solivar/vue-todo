<template>
  <form @submit.prevent="onSubmit">
    <div class="group">
      <label for="title">Add task: </label>
      <input id="title" type="text" v-model="title">
      <button type="submit">Add</button>
    </div>
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
        this.error = 'Task title must be 2-50 characters long';

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

.group {
  display: flex;
  align-items: center;
}

form {
  margin-bottom: 30px;
}

label {
  flex: 0 0 75px;
}

input {
  border: 1px solid $grey;
  padding: 4px 10px;
  height: 30px;
  box-sizing: border-box;
  border-radius: 5px;
  margin-right: 5px;
  flex: 1 1 auto;
}

button {
  background: $green;
  color: #ffffff;
  border: 0;
  height: 30px;
  padding: 0;
  border-radius: 10px;
  font-weight: bold;
  text-transform: uppercase;
  flex: 0 0 80px;

  &:hover, &:active {
    background: darken($color: $green, $amount: 5%);
    cursor: pointer;
  }
}

.error {
  margin: 10px 0 0;
}

@media screen and (max-width: 500px) {
  .group {
    flex-wrap: wrap;

    label, input {
      flex: 1 1 100%;
      margin: 0 0 10px;
    }

    button {
      flex: 1 1 100%;
    }
  }
}
</style>
