<template>
  <div id="app">
    <div class="container">
      <h1 class="heading">ToDo</h1>
      <TaskCounter :count="tasks.length" />
      <TaskForm @addTask="addTask" :count="tasks.length" />
      <TaskList
        :tasks="tasks"
        @deleteTask="deleteTask"
        @toggleCompletion="toggleCompletion"
      />
    </div>
  </div>
</template>

<script>
import TaskCounter from './components/TaskCounter';
import TaskForm from './components/TaskForm';
import TaskList from './components/TaskList';

export default {
  name: 'App',
  components: {
    TaskCounter,
    TaskForm,
    TaskList
  },
  data: () => {
    return {
      tasks: [
        {
          id: new Date() - 1000,
          title: 'Learn VueJS',
          isCompleted: false,
        },
        {
          id: +new Date(),
          title: 'Read book',
          isCompleted: true,
        },
      ],
    };
  },
  methods: {
    addTask: function(title) {
      const task = {
        id: +new Date(),
        title,
      }

      this.tasks = [...this.tasks, task];
    },
    deleteTask: function (id) {
      const tasks = this.tasks.filter(task => {
        return task.id !== id;
      })

      this.tasks = tasks;
    },
    toggleCompletion: function(id) {
      const tasks = this.tasks.map(task => {
        if (task.id === id) {
          task.isCompleted = !task.isCompleted;
        }

        return task;
      })

      this.tasks = tasks;
    }
  }
}
</script>

<style lang="scss">
@import './styles/variables';

html {
  height: 100%;
}

body {
  margin: 0;
  padding: 0;
  height: 100%;
  background-color: $white;
  font-family: 'Lato', sans-serif;
  }

#app {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.heading {
  margin: 0 auto 30px;
  text-align: center;
  padding-bottom: 10px;
  border-bottom: 2px solid $green;
}

.container {
  margin: 0 10px;
  width: 100%;
  max-width: 500px;
  background-color: #ffffff;
  border: 1px solid $grey;
  border-radius: 5px;
  padding: 30px;
  box-shadow: 0px 10px 25px 0px rgba(0,0,0,0.2), 0px 5px 5px 0px rgba(0,0,0,0.1);
}
</style>
