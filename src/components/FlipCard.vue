<template>
    <div id="flip-card">
      <div class="flip-card">
        <div class="flip-card-inner">
          <div class="flip-card-front">
            <img 
              :src="srcFront"
              :alt="frontName"
              :class="frontName"  
            />
          </div>
          <div class="flip-card-back">
            <img 
              :src="srcBack"
              :alt="backName"
              :class="backName"
            />
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { computed } from 'vue';
  
  export default {
    name: "flip-card",
    props: ['folder', 'frontName', 'backName'],
    setup(props) {
      const srcFront = computed(() => {
        return new URL(`../assets/media/${props.folder}/${props.frontName}.png`, import.meta.url).href;
      });
  
      const srcBack = computed(() => {
        return new URL(`../assets/media/${props.folder}/${props.backName}.png`, import.meta.url).href;
      });
  
      return {
        srcFront,
        srcBack
      };
    }
  };
  </script>
  
  <style scoped>
  .flip-card {
    width: 30vw;
    height: 20vh;
    margin: 0 auto;
  }
  
  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.8s ease-in-out; /* Smooth flip transition */
    transform-style: preserve-3d;
  }
  
  .flip-card:hover .flip-card-inner {
    transform: rotateY(180deg); /* Flips the card on hover */
  }
  
  .flip-card-front, .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
  }
  
  .flip-card-back {
    transform: rotateY(180deg);
    position: relative;
    top: 0.45vh;
    right: 0.195vw;
  }
  
  .target-front {
    position: absolute;
    top: 10vh;
    left: 50%;
    transform: translateX(-50%);
    width: 30vw;
  }
  
  .target-back {
    position: absolute;
    top: 10vh;
    left: 50%;
    transform: translateX(-50%);
    width: 30vw;
  }
  </style>
  