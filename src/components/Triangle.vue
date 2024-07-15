<template>
    <div id="triangle">
      <navbar :titleIndex="1" @switch-page="switchPage"></navbar>
    </div>
  </template>
  
  <script>
  import Navbar from '@/components/Navbar.vue';
  
  export default {
    name: "triangle",  
    props: ['whereBeen'],
    components: {
      Navbar
    },
    emits: ['switch-screen', 'switch-page'],  
    methods: {
      nextPage() {
        this.$emit("switch-screen", 4);
      },
      switchPage(index) {
        if (this.whereBeen.includes(index)) {
          this.$emit('switch-screen', index);
        }
      },
    }
  }
  </script>
  
  <style scoped>
  #triangle {
    font-family: "Heebo";
    text-align: center;
    display: flex;
    justify-content: center;
  }
  </style>
  