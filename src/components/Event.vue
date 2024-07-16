<template>
    <div id="event">
      <navbar :titleIndex="2" @switch-page="switchPage"></navbar>
      <div class="title">אירוע החניכה</div>

    </div>
  </template>
  
  <script>
  import Navbar from '@/components/Navbar.vue';
  
  export default {
    name: "event",  
    props: ['whereBeen'],
    components: {
      Navbar
    },
    emits: ['switch-screen', 'switch-page'],  
    data() {
      return {
       
      };
    },
    methods: {
      nextPage() {
        this.$emit("switch-screen", 5);
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
  #event {
    font-family: "Heebo";
    text-align: center;
    display: flex;
    justify-content: center;
  }
  
  .title {
    font-size: 4rem;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 11rem;
    font-family: 'Heebo-bold';
    color: #0077B6;
    width: 100vw;
  }
  
  </style>
  