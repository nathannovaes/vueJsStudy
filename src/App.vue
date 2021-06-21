<template>
  <div class="container">
    <Header @show-form="showForm" title="Lista de tarefas"/>
    <div v-if="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="reminderTask"  @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';


export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    },
    reminderTask(id) {
      this.tasks = this.tasks.map((task) => task.id === id ? { ...task, reminder: !task.reminder } : task)
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    showForm() {
      this.showAddTask = true
    }
  },
  created() {
    this.tasks = [
      {
        id: 1, 
        text: 'Medico',
        day: '21/06/2021 as 15h00',
        reminder: true
      },
      {
        id: 2, 
        text: 'Aniversario',
        day: '24/06/2021 as 20h00',
        reminder: false
      },
      {
        id: 3, 
        text: 'Nutricionista',
        day: '26/06/2021 as 10h00',
        reminder: false
      },
      {
        id: 4, 
        text: 'Meetup',
        day: '29/06/2021 as 19h30',
        reminder: false
      },
      {
        id: 5, 
        text: 'Mercado',
        day: '30/06/2021 as 18h30',
        reminder: false
      }
    ]
  }
}
</script>

<style>
 @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

 * {
   box-sizing: border-box;
   margin: 0;
   padding: 0;
 }

 body {
   font-family: 'Poppins', sans-serif;
 }

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background-color: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}  
.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
