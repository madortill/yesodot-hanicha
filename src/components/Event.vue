<template>
    <div id="event">
      <navbar :titleIndex="2" @switch-page="switchPage"></navbar>
      <div class="title"> {{ slidesInfo[curSlide].title }}</div>
      <div class="text"> {{ slidesInfo[curSlide].text }}</div>

      <div v-if="curSlide === '1'">
        <img 
          src="../assets/media/event/heart.png" 
          alt="heart"
          class="heart" 
          @click="changeMe"/>

          <img v-for="i in 3" :key="i" :class="{ [`arrow-${i}`]: true, arrow: true }" src="../assets/media/event/arrow.svg"/>
          <div v-for="(title, index) in array" :key="index" :class="['titles', `title-${index}`]"> {{ title }} </div>
          <div class="subtitle">תראו ללב קצת אהבה ולחצו עליו</div>

          <div class="container" v-show="showWindow">
              <div class="close" @click="changeMe">x</div>
              <div>חניכה על תפקיד  VS חניכה על ביצוע </div>
              <div>לחצו על סוגי החניכה כדי לגלות מה ההבדלים ביניהם</div>
              <img src="../assets/media/event/boy-soilder.png"/>
              <img  src="../assets/media/event/girl-soilder.png"/>
          </div>
      </div>
     
      <!-- <triangle></triangle> -->
      <button v-if="showButton" class="button next" @click="nextTitle">המשך</button>
      <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
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
       showWindow: false,
       didClick: false,
       curSlide: '1',
       slidesInfo: {
        '1': {
          title: 'לב האירוע',
          text: 'המיומנות המרכזית עליה מבצעים תהליך חניכה'
        },
        '2': {
          title: 'מעגל החניכה',
          text: 'מודל המתאר שלבים של תהליך החניכה על ביצוע בודד'
        },
        '3': {
          title: 'מודל החניכה על תפקיד',
          text: ''
        }
      }
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
      changeMe() {
        this.showWindow = !this.showWindow;
        this.didClick = true;
      },
      nextTitle() {
        let slideNum = Number(this.curSlide);
        slideNum++;
        this.curSlide = String(slideNum);
      },
      lastTitle() {
        let slideNum = Number(this.curSlide);
        slideNum--;
        this.curSlide = String(slideNum);
      },
  },
  computed: {
    showButton() {
      return this.curSlide !== '3' && (this.curSlide === '1' ? this.didClick && !this.showWindow : true);
    }
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

  .next {
  position: absolute;
  bottom: 12%;
  left: 20%;
}

.back {
  position: absolute;
  bottom: 12%;
  right: 10%;
}

.button {
  transform: translateX(-50%);
  cursor: pointer;
  color: #fff;
  background-color: #0492bd;
  border: none;
  border-radius: 100px;
  font-family: "Heebo";
  width: 11rem;
  font-size: 1.5rem;
  padding: 1rem;
  animation: borderPulse 4000ms infinite ease-out;
}


.button:hover,
.button:focus {
  animation: borderPulse 4000ms infinite ease-out, hoverShine 200ms;
}

@keyframes borderPulse {
  0% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255, .4), 0px 0px 0px 0px rgba(255, 255, 255, 1);
  }
  35% {
    box-shadow: inset 0px 0px 0px 3px rgba(117, 117, 255, .2), 0px 0px 0px 10px rgba(255, 255, 255, 0);
  }
  50% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255, .4), 0px 0px 0px 0px rgba(255, 255, 255, 1);
  }
  75% {
    box-shadow: inset 0px 0px 0px 3px rgba(117, 117, 255, .2), 0px 0px 0px 10px rgba(255, 255, 255, 0);
  }
  100% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255, .4), 0px 0px 0px 0px rgba(255, 255, 255, 1);
  }
}

@keyframes hoverShine {
  0% {
    background-image: linear-gradient(135deg, rgba(255, 255, 255, .4) 0%, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0) 100%);
  }
  50% {
    background-image: linear-gradient(135deg, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, .4) 50%, rgba(255, 255, 255, 0) 100%);
  }
  100% {
    background-image: linear-gradient(135deg, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, .4) 100%);
  }
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
    /* filter: sepia(1) saturate(2) hue-rotate(175deg); */
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

.container {
  background-color: white;
  width: 70vw;
  height: 70vh;
  position: absolute;
  top: 20vh;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 7vw;
  z-index: 3;
}

.close {
  position: absolute;
  top: 3%;
  right: 6%;
  font-size: 3rem;
  cursor: pointer;
}
  </style>
  