<template>
    <div id="triangle">
      <navbar :titleIndex="1" @switch-page="switchPage"></navbar>
      <div class="title">לתהליך החניכה ישנם שלושה גורמים משפיעים</div>
      <img v-for="(item, index) in array" 
      :key="index" 
      :class="item" 
      :src="imageSrc(item)"
      :alt="item"
      @click="item === 'subject1' ? nextPage() : null"
      />
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
    data() {
      return {
        array: ['triangle', 'subject1', 'subject2', 'subject3'],
      };
    },
    methods: {
      nextPage() {
        this.$emit("switch-screen", 4);
      },
      switchPage(index) {
        if (this.whereBeen.includes(index)) {
          this.$emit('switch-screen', index);
        }
      },
      imageSrc(item) {
        return new URL(`../assets/media/triangle/${item}.png`, import.meta.url).href;
      }
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
  .subject1 {
    position: absolute;
    top: 35vh;
    cursor: pointer;
    animation: pulse-smaller 1.5s infinite;
}

@keyframes pulse-smaller {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}

  .subject2 {
    position: absolute;
    bottom: 20vh;
    right: 35vw;
  }
  .subject3 {
    position: absolute;
    bottom: 20vh;
    left: 35vw;
  }
  .triangle {
    position: absolute;
    top: 40vh;
    width: 24vw;
  }
  </style>
  