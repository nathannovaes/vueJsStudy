<template>
  <button @click="onClick" class="btn" :class="color" ><i :class="[icon, 'fa']"></i></button>  
</template>

<script>
  export default {
    name: 'Button',
    props: {
      icon: {
        type: String
      },
      color: {
        type: String
      }
    },
    methods: {
      onClick() {
        this.$emit('btn-click')
      }
    }
  }
</script>

<style scoped>
  .green {
    background-color: darkgreen;
  }

  .red {
    background-color: darkred;
  }

  .blue {
    background-color: steelblue;
  }
</style>