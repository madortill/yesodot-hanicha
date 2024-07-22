<template>
    <div id="event">
      <navbar :titleIndex="2" @switch-page="switchPage"></navbar>
      <div class="title">לב האירוע</div>
      <div class="text">המיומנות המרכזית עליה מבצעים תהליך חניכה</div>
      <img src="../assets/media/event/heart.png" alt="heart" class="heart"/>
      <img v-for="i in 3" :key="i" :class="{ [`arrow-${i}`]: true, arrow: true }" src="../assets/media/event/arrow.svg"/>
      <div v-for="(title, index) in array" :key="index" :class="['titles', `title-${index}`]"> {{ title }} </div>
      <div class="subtitle">תראו ללב קצת אהבה ולחצו עליו</div>
      <!-- <triangle></triangle> -->

    </div>
  </template>
  
  <script>
   import Navbar from './Navbar.vue';
   import Triangle from './Triangle.vue'
  export default {
    name: "event",  
    props: ['whereBeen'],
    components: {
      Navbar,
      Triangle
    },
    emits: ['switch-screen', 'switch-page'],  
    data() {
      return {
       array: ["ביצוע מוטורי", "ביצוע קוגנטיבי", "ביצוע רגשי"],
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
    overflow-x: hidden; 
    overflow-y: hidden; 
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

  @keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}


  .heart {
    position: fixed;
    left: 10vw;
    bottom: 0vh;
    width: 40vw;
    filter: sepia(1) saturate(2) hue-rotate(175deg);
    animation: pulse 2s infinite;
    cursor: pointer;
  }
  
  .text {
  position: absolute;
  right: 1vw;
  top: 18rem;
  font-size: 2rem;
  width: 60vw;
}

.arrow {
  width: 6vw;
}

.arrow-1 {
  position: absolute;
  bottom: 30vh;
  left: 38vw;
  rotate: 120deg;
}

.arrow-2 {
  position: absolute;
  left: 36vh;
  bottom: 10vh;
  rotate: 290deg;
}
.arrow-3 {
  position: absolute;
  left: 28vh;
  bottom: 47vh;
}

.title-0 {
  position: absolute;
  left: 7vw;
  bottom: 14vh;
}

.title-1 {
  position: absolute;
  left: 9vw;
  top: 35vh;
}

.title-2 {
  position: absolute;
  right: 47vw;
  bottom: 33vh;
}

.titles {
   font-size: 2.2rem;
   color: #03045E;
}

.subtitle {
  position: absolute;
  left: 22vw;
  bottom: 2rem;
  font-size: 1.4rem;
  color: rgb(241, 108, 89);
  animation: pulse 2s infinite;
}
  </style>
  