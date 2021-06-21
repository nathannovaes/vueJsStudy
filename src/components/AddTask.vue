<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" name="text" v-model="text" placeholder="Adicione uma tarefa"/>
    </div>
    <div class="form-control">
      <label>Data e Hora</label>
      <input type="text" name="day" v-model="day" placeholder="Adicione uma data e hora"/>
    </div>
    <div class="form-control form-control-check">
      <div>Lembrar</div>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>
    <input type="submit" value="Salvar Tarefa" class="btn btn-block"/>
  </form>
</template>
<script>
import Button from './Button.vue'
  export default {
  components: { Button },
    name: 'AddTask',
    data() {
      return {
        text: '',
        day: '',
        reminder: false
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault();

        this.formValidation();
      
        const newTask = {
          id: Math.floor(Math.random() * 100000),
          text: this.text,
          day: this.day,
          reminder: this.reminder
        } 

        this.$emit('add-task', newTask);

        this.clearForm();
      }, 
      clearForm() {
        this.text = '',
        this.day = '',
        this.reminder = ''
      },
      formValidation() {
        if(!this.text || !this.day) {
          throw new Error("Por favor, preencha os todos os campos.");
        }
      }
    }
  }
</script>

<style scoped>
  .add-form {
    margin-bottom: 40px;
  }

  .form-control {
    margin: 20px 0;
  }

  .form-control label {
    display: block;
  }
  
  .form-control input {
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
  }

  .form-control-check {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .form-control-check label {
    flex: 1;
  }

  .form-control-check input {
    flex: 2;
    height: 20px;
  }


</style>