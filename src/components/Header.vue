<template>
  <header>
    <h1>{{ title }}</h1>  
      <Button @show-form="$emit('show-form')" color="green" icon="fa-plus"/>
  </header>
</template>

<script>
  import Button from "./Button.vue"

  export default {
    name: 'Header',
    props: {
      title: {
        type: String,
        default: 'Hello world.'
      }
    },
    components: {
      Button,
    },
    emits: ['show-form']
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