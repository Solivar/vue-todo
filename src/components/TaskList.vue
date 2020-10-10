<template>
  <ul>
    <li v-for="task in tasks" v-bind:key="task.id">
      <TaskItem v-bind="task" />
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
      validator: task => {
        return task.id && task.title;
      }
    }
  }
}
</script>
<style scoped>
</style>
