<template>
    <div id="triangle">
      <div class="title">לתהליך החניכה ישנם שלושה גורמים משפיעים</div>
      <img v-for="(item, index) in array" 
      :key="index" 
      :class="[item , item === wherePulse ? 'pulse' : 'item']"
      :src="imageSrc(item)"
      :alt="item"
      @click="item === wherePulse ? nextPage() : null"
      />
    </div>
  </template>
  
  <script>
  
  
  export default {
    name: "triangle",  
    props: ['wherePulse'],
    emits: ['switch-screen', 'switch-page'],  
    data() {
      return {
        array: ['triangle', 'event', 'educated', 'educator'],
      };
    },
    methods: {
      nextPage() {
        if (this.wherePulse === "event") {
          this.$emit("switch-screen");
        } else if (this.wherePulse === "educated") {
          this.$emit("switch-screen");
        }  else if (this.wherePulse === "educator") {
          this.$emit("switch-screen");
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
  .event {
    position: absolute;
    top: 35vh;
}

.pulse {
  animation: pulse-smaller 1.5s infinite;
  cursor: pointer; 
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

  .educated {
    position: absolute;
    bottom: 20vh;
    right: 35vw;
  }
  .educator {
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
  