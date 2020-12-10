<template>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      <TaskItem :task="task"
        @deleteTask="deleteTask"
        @toggleCompletion="toggleCompletion"
        @updateTask="updateTask"
      />
    </li>
  </ul>
</template>

<script>
import TaskItem from './TaskItem';
export default {
  name: 'TaskList',
  components: {
    TaskItem,
  },
  props: {
    tasks: {
      type: Array,
      default: () => [],
      validator: tasks => {
        tasks.forEach(task => {
          if (!task.id || !task.title) {
            return false;
          }
        });

        return true;
      }
    }
  },
  methods: {
    deleteTask: function(id) {
      this.$emit('deleteTask', id)
    },
    toggleCompletion: function(id) {
      this.$emit('toggleCompletion', id);
    },
    updateTask: function(task) {
      this.$emit('updateTask', task);
    }
  }
}
</script>
<style scoped lang="scss">
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

</style>
