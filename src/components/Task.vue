<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fas fa-trash"></i>  
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Task',
    props: {
      task: Object
    },
    methods: {
      onDelete(id) {
        this.$emit('delete-task', id);
      }
    }
  }
</script>

<style scope>
  .fas {
    font-size: 12px;
    color: rgba(255, 0, 0, 0.500);
  }
  .task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }

  .task.reminder {
    border-left: 8px solid green;
  }

  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }


</style>