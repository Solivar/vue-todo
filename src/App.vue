<template>
  <div id="app">
    <div class="container">
      <h1>ToDo</h1>
      <TaskCounter :count="tasks.length" />
      <TaskForm />
      <TaskList :tasks="tasks" />
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
        },
        {
          id: +new Date(),
          title: 'Read book',
        },
      ],
    };
  }
}
</script>

<style>
  html {
    height: 100%;
  }

  body {
    margin: 0;
    padding: 0;
    height: 100%;
    background-color: #32498C;
  }

  #app {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  h1 {
    margin: 0;
  }

  .container {
    margin: 0 10px;
    width: 100%;
    max-width: 800px;
    background-color: #ffffff;
    border-radius: 10px;
    padding: 30px;
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.2);
  }
</style>
