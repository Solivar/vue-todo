<template>
  <ul>
    <li v-for="task in tasks" v-bind:key="task.id">
      <TaskItem v-bind="task" @deleteTask="deleteTask"/>
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
    }
  }
}
</script>
<style scoped>
</style>
