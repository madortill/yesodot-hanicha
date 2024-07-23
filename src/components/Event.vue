<template>
    <div id="event">
      <navbar :titleIndex="2" @switch-page="switchPage"></navbar>
      <div class="title"> {{ slidesInfo[curSlide].title }}</div>
      <div :class="{ text: true, right: curSlide === '1', subtext: curSlide === '2' }"> {{ slidesInfo[curSlide].text }}</div>

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
              <div class="title inner">סוגי ביצועים</div>
              <div class="subtitle inside">עברו עם העכבר מעל הסוגים השונים כדי ללמוד עליהם</div>
          </div>
      </div>

      <div v-else-if="curSlide === '2'">
              <img class="boy solider" src="../assets/media/event/boy-solider.png"/>
              <div class="subject2" @click="openMeOnce">ביצוע</div>
              <div class="once-container">
                <div v-show="showMeForOnce" class="info-container">
                  <div v-for="item in arrayInfoOnce" :key="item">
                    {{ item }}
                  </div>
                </div>
              </div>

              <img class="girl solider" src="../assets/media/event/girl-solider.png"/>
              <div class="subject1" @click="openMeAlways">תפקיד</div>
              <div class="always-container">
                <div v-show="showMeForAlways" class="info-container">
                  <div v-for="item in arrayInfoAlways" :key="item">
                    {{ item }}
                  </div>
                </div>
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
          title: ' חניכה על תפקיד  VS חניכה על ביצוע  ',
          text: 'לחצו על סוגי החניכה כדי לגלות מה ההבדלים ביניהם'
        },
        '3': {
          title: 'מעגל החניכה',
          text: ''
        },
        '4': {
          title: 'מודל החניכה על תפקיד',
          text: ''
        }
      },
      arrayInfoOnce: ['זמן קצר - ימים עד שבועות', 'ביצוע בודד בעל גורם משפיע אחד', 'מומחה תוכן לביצוע', 'חשובה אך לא הכרחית'],
      arrayInfoAlways: ['זמן ארוך יחסית - שבועות עד שנים', 'מספר ביצועים בעלי גורמים משפיעים', 'לא תמיד צריך מומחה תוכן לכל ביצוע', 'קריטית והכרחית'],
      arraySubjects: ['משך החניכה','מורכבות החניכה','מומחיות החונך','תקשורת בין החונך לנחנך'],
      showMeForOnce: false,
      showMeForAlways: false,
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
      openMeOnce() {
        this.showMeForOnce = true;
      },
      openMeAlways() {
        this.showMeForAlways= true;
      }
  },
  computed: {
    showButton() {
      return this.curSlide !== '4' && (this.curSlide === '1' ? this.didClick && !this.showWindow : true);
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
  left: 50%;
  transform: translateX(-50%);
  top: 20rem;
  font-size: 2rem;
  width: 60vw;
}
.text.right {
  left: auto;  /* Override left */
  transform: none;  /* Override transform */
  right: 1vw !important;
}

.inner {
  position: absolute;
  top: 5vh;
}

.inside {
  animation: none !important;
  position: absolute;
  top: 14vh;
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
  left: 30vh;
  bottom: 20vh;
  rotate: 290deg;
}
.arrow-3 {
  position: absolute;
  left: 28vh;
  bottom: 47vh;
}
.subtext{
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 16rem;
  font-size: 1.4rem;
  color: rgb(241, 108, 89);
}
.title-0 {
  position: absolute;
  left: 4vw;
  bottom: 24vh;
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

.solider {
  width: 7vw;
}

.boy {
  position: absolute;
  right: 18.5vw;
  top: 31vh;
}

.girl {
  position: absolute;
  left: 17vw;
  top: 31vh;
}

@keyframes float {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
  100% {
    transform: translateY(0);
  }
}

.subject1,
.subject2 {
  animation: float 3s ease-in-out infinite;
}

/* Hover effect for info-container items */
.info-container div:hover {
  background-color: rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease;
  border-radius: 12vmax;
}

/* Animation for the info-container */
@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.info-container {
  width: 19vw;
  height: 31vh;
  padding: 1vw;
  background-color: white;
  border-radius: 4vmax;
  font-size: 1.48rem;
  animation: slideIn 0.5s ease-out;
  display: flex;
  flex-direction: column;
  align-items: center; /* Center items horizontally */
  gap: 1vw; /* Adjust this value for spacing between items */
}

/* Add margin to each item inside the info-container */
.info-container > div {
  width: 100%; /* Make sure items fill the container width */
  text-align: center; /* Center text */
  padding: 0.5vw; /* Adjust padding as needed */
}

/* Hover effect for info-container items */
.info-container div:hover {
  background-color: rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease;
  border-radius: 12vmax;
}

.once-container {
  position: absolute;
  top: 42vh;
  left: 24vw;
}

.always-container {
  position: absolute;
  top: 42vh;
  right: 24vw;
}

.subject1 {
  font-family: "Heebo-bold";
  font-size: 3rem;
  color:#03045E;
  position: absolute;
  top: 34vh;
  right: 31vw;
  cursor: pointer;
}

.subject2 {
  font-family: "Heebo-bold";
  font-size: 3rem;
  color:#03045E;
  position: absolute;
  top: 34vh;
  left: 31.5vw;
  cursor: pointer;
}
  </style>
  