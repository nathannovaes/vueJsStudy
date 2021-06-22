<template>
  <header>
    <h1>{{ title }}</h1>  
    <Button @btn-click="$emit('toggle-form-button')" 
    :color="changeButtonContent? 'red' : 'green'" 
    :icon="changeButtonContent ? 'fa-times' : 'fa-plus'"/>
  </header>
</template>

<script>
  import Button from "./Button.vue"

  export default {
    name: 'Header',
    props: {
      title: String,
      changeButtonContent: Boolean
    },
    components: {
      Button,
    },
    emits: ['toggle-form-button']
  }
</script>

<style scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
</style>