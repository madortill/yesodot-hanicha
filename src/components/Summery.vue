<template>
    <div id="summery">
      <canvas ref="confettiCanvas"></canvas>
      <div class="title">{{ slidesInfo[curSlide].title }}</div>
      <div :class="{ text: true }" v-html="slidesInfo[curSlide].text"></div>
    </div>
  </template>
  
  <script>
  import confetti from 'canvas-confetti';
  
  export default {
    name: "summery",
    data() {
      return {
        curSlide: '1',
        slidesInfo: {
          '1': {
            title: 'סיכום',
            text: '<br>למדנו מהי חניכה, מהן מטרותיה, העמקנו בנושא "אירוע החניכה" והגורמים המשפיעים עליו (חונך ונחנך). <br><br>עד עכשיו עברתם את הלומדה הראשונה מתוך חמש, בהצלחה!'
          },
        }
      };
    },
    mounted() {
      this.launchConfetti();
    },
    methods: {
      launchConfetti() {
        const canvas = this.$refs.confettiCanvas;
        const myConfetti = confetti.create(canvas, { resize: true });
        
        const confettiSettings = {
          particleCount: 300,
          spread: 180,
          origin: { y: 0.6 }
        };
  
        const intervalId = setInterval(() => {
          myConfetti(confettiSettings);
        }, 2500); // Repeat every 2 seconds
  
        // Clear the interval when the component is destroyed to prevent memory leaks
        this.$once('hook:beforeDestroy', () => {
          clearInterval(intervalId);
        });
      }
    }
  };
  </script>
  
  <style scoped>
  #summery {
    font-family: "Heebo";
    text-align: center;
    display: flex;
    justify-content: center;
    overflow-x: hidden;
    overflow-y: hidden;
    position: relative;
    height: 100vh; /* Ensure the container takes up the full height of the viewport */
  }
  
  canvas {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 0; /* Behind the text */
  }
  
  .title, .text {
    z-index: 1; /* In front of the canvas */
    position: absolute; /* Ensure proper stacking context */
  }
  
  .title {
    font-size: 4rem;
    left: 50%;
    transform: translateX(-50%);
    top: 3rem;
    font-family: "Heebo-bold";
    color: #0077b6;
    width: 100vw;
  }
  
  .text {
    left: 50%;
    transform: translateX(-50%);
    top: 9rem;
    font-size: 2rem;
    width: 60vw;
  }
  </style>
  