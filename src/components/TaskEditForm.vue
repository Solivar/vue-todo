<template>
  <form @submit.prevent="onSubmit">
      <div class="group">
        <input id="title" ref="title" v-model="newTitle" @blur="onSubmit">
      </div>
  </form>
</template>

<script>
export default {
  name: 'TaskForm',
  props: {
    title: String,
  },
  data: function() {
    return {
      newTitle: this.title,
    }
  },
  mounted() {
    this.focusInput();
  },
  methods: {
    focusInput: function() {
      this.$refs.title.focus();
    },
    onSubmit: function () {
      if (this.newTitle.length < 2 || this.newTitle.length > 50) {
        return;
      }

      this.$emit('editTitle', this.newTitle);
    }
  }
}
</script>
<style scoped lang="scss">
@import '../styles/variables';

.group {
  display: flex;
}

.error {
  margin: 10px 0 0;
}

input {
  border: 0;
  margin: 0 10px;
  padding: 0;
  width: 100%;
  min-width: 50px;
  font-size: 16px;
  font-family: "Lato", sans-serif;
}
</style>
