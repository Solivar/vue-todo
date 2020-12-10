<template>
  <div class="task">
    <div class="completion">
      <input type="checkbox"
        @change="toggleCompletion"
        :checked="task.isCompleted"
      >
    </div>
    <p
      class="title"
      v-show="!isEditingEnabled"
      v-bind:class="{ striked: task.isCompleted }"
      @click="toggleEditing"
    >
      {{ task.title }}
    </p>
    <div class="task-edit" v-if="isEditingEnabled">
      <TaskEditForm :title="task.title" @editTitle="editTitle" />
    </div>
    <div v-show="!isEditingEnabled" class="edit-container" @click="toggleEditing">
      <button>Edit</button>
    </div>
    <button class="delete" @click="deleteTask">X</button>
  </div>
</template>

<script>
import TaskEditForm from './TaskEditForm';

export default {
  name: 'TaskItem',
  components: {
    TaskEditForm,
  },
  data: () => {
    return {
      isEditingEnabled: false,
    };
  },
  props: {
    task: {
      id: Number,
      title: String,
      isCompleted: Boolean,
    }
  },
  methods: {
    deleteTask: function() {
      this.$emit('deleteTask', this.task.id);
    },
    toggleCompletion: function() {
      this.$emit('toggleCompletion', this.task.id);
    },
    toggleEditing: function() {
      this.isEditingEnabled = !this.isEditingEnabled;
    },
    editTitle: function(newTitle) {
      const updatedTask = Object.assign({}, { ...this.task, title: newTitle });

      this.toggleEditing();
      this.$emit('updateTask', updatedTask);
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
  height: 41px;
  box-sizing: border-box;
  position: relative;

  &:hover {
    .edit-container {
      opacity: 1;
    }
  }
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
  cursor: pointer;
  font-weight: bold;
  border: none;
  color: $blue;
  background: none;
}

button.delete {
  border-left: 1px solid $grey;
  padding: 0 10px;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin: -10px -10px -10px 0;

  &:hover, &:active {
    color: $red;
  }
}

.task-edit {
  flex: 1 1 100%;
}

.edit-container {
  opacity: 0;
  position: absolute;
  right: 30px;
  color: $blue;

  font-weight: bold;
  display: inline-block;
  width: auto;
  text-align: center;
  padding: 0;
  background-color: #ffffff;

  button {
    text-transform: uppercase;
    padding: 0 30px;
  }
}
</style>
