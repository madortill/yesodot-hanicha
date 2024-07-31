<template>
    <div id="educated">
      <div v-if="!showComponent">
      <div class="title">{{ slidesInfo[curSlide].title }}</div>
      
      <div v-if="!clicked" id="clickMe" @click="showInfo">
       <p>לחצו עליי</p>
     </div>
     <div id="disappearing"> עברו בכל השלבים עד שיהפכו לירוקים </div>

      <div class="pictures-container">
        <div class="right-container">
          <div v-for="(value, key) in rightSubjcets" :key="key" :id="key" :class="['subject', isGreen[key] ? 'green' : '']" @click="goHere">
            {{ value }}
          </div>
        </div>
        <div class="left-container">
          <div v-for="(value, key) in leftSubjcets" :key="key" :id="key" :class="['subject', isGreen[key] ? 'green' : '']" @click="goHere">
            {{ value }}
          </div>
        </div>
        <div class="flip-card flip-card-left">
          <div class="flip-card-inner">
            <div class="flip-card-front">
              <img src="../assets/media/educated/personal-traits.png"/>
            </div>
            <div class="flip-card-back">
              <div class="title-text">מאפיינים אישיים</div>
            </div>
          </div>
        </div>
  
        <div class="flip-card flip-card-right">
          <div class="flip-card-inner">
            <div class="flip-card-front">
              <img src="../assets/media/educated/abilities.png"/>
            </div>
            <div class="flip-card-back">
              <div class="title-text">יכולות וכישורים</div>
            </div>
          </div>
        </div>
      </div>
      </div>
     
      <component v-else :componentName="whereToGoNow" :is="whereToGoNow" @add-green="addGreen"></component>
      <div id="yalla-next" v-if="allGreen" @click="nextPage"></div>

    </div>
  </template>
  
  <script>
  
  import LearningHabbits from './LearningHabbits.vue'; 
import Motivation from './Motivation.vue'; 
import FeelingCapable from './FeelingCapable.vue'; 
import Advanced from './Advanced.vue'; 
import Job from './Job.vue'; 
import ThinkingStyles from './ThinkingStyles.vue'; 
  
  export default {
    name: "educated",
    components: {
      LearningHabbits,
      Motivation,
      FeelingCapable,
      Advanced,
      Job,
      ThinkingStyles
    },
    emits: ['switch-screen', 'switch-page'],
    data() {
      return {
        slidesInfo: {
          '1': {
            'title': 'בתור חונכים, עלינו לנתח ולאפיין שני היבטים של הנחנך',
            'text': ''
          },
          whereClicked: [],
        },
        curSlide: '1',
        rightSubjcets: {
          'ThinkingStyles' : 'סגנונות חשיבה ולמידה',
          'Job' : 'תפיסת תפקיד',
          'Advanced' : 'ניסיון קודם בתהליך חניכה'
        },
        leftSubjcets: {
          'LearningHabbits' : 'הרגלי למידה',
          'Motivation' : 'מוטיבציה',
          'FeelingCapable' : 'תחושת מסוגלות עצמית'
        } ,
        clicked: false,
        showComponent: false,
        whereToGoNow :'',
        whereGreen: [],
        isGreen: {
          LearningHabbits: false,
          Motivation: false,
          FeelingCapable: false,
          Advanced: false,
          Job: false,
          ThinkingStyles: false
        }
      };
    },
    computed: {
      allGreen() {
      const allTrue = Object.values(this.isGreen).every(value => value === true);
      return allTrue;
    }
  },
    methods: {
      nextPage() {
        this.$emit("switch-screen");
      },
    showInfo() {
      console.log("Showing info"); // Debugging line
      setTimeout(() => {
        this.clicked = true;
      }, 3500);
      document.getElementById("clickMe").classList.add("clicked");
        const disappearingMsg = document.getElementById("disappearing");
        disappearingMsg.classList.add("show");
        document.getElementById("clickMe").classList.add("disappear");
    },
    goHere(event) {
      this.whereToGoNow = event.currentTarget.id;
      this.showComponent = true;
    },
    addGreen(componentName) {
      this.showComponent = false;
      this.isGreen[componentName] = true;
    },
    }
}
  </script>
  
<style scoped>
#educated {
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

.text {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 20rem;
  font-size: 2rem;
  width: 60vw;
}

.pictures-container {
  display: flex;
  position: absolute;
  top: 60%;
  left: 50%;
  width: 50vw; /* Increased width */
  justify-content: space-evenly;
  transform: translate(-50%, -50%);
}

.flip-card {
  background-color: transparent;
  width: 15vw; /* Increased size */
  height: 15vw; /* Increased size */
  perspective: 1000px;
  padding: 3vw;
  animation: cardSizeAnimation 4s forwards; /* Initial size animation */
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 3s; /* Flip duration */
  transform-style: preserve-3d;
  border-radius: 50%;
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: transparent;
}

.flip-card-front img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
}

.flip-card-back {
  background-color: rgb(83, 83, 141);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: rotateY(180deg);
}

.title-text {
  font-size: 3rem;
  text-align: center;
}

.flip-card-left .flip-card-inner {
  animation: flipCardLeft 4s forwards; /* Flip direction */
}

.flip-card-right .flip-card-inner {
  animation: flipCardRight 4s forwards; /* Flip direction */
}

@keyframes cardSizeAnimation {
  0% {
    transform: scale(1.5); /* Start larger */
  }
  100% {
    transform: scale(1); /* End at normal size */
  }
}

@keyframes flipCardLeft {
  0% {
    transform: rotateY(0deg);
  }
  50% {
    transform: rotateY(180deg);
  }
  100% {
    transform: rotateY(180deg);
  }
}

@keyframes flipCardRight {
  0% {
    transform: rotateY(0deg);
  }
  50% {
    transform: rotateY(-180deg);
  }
  100% {
    transform: rotateY(-180deg);
  }
}
.right-container, .left-container {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 20vw; /* Adjust width as needed */
}

.right-container {
  right: -12vw; /* Adjust positioning as needed */
}

.left-container {
  left: -12vw; /* Adjust positioning as needed */
}

.subject {
  background-color: white;
  border-radius: 50px;
  color: rgb(83, 83, 141);
  font-size: 1.2rem;
  padding: 1.3vw;
  cursor: pointer;
  margin: 0.5rem 0; /* Add margin for spacing between subjects */
}

@keyframes slideInFromRight {
  from {
    transform: translateX(100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

@keyframes slideInFromLeft {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.right-container .subject {
  animation: slideInFromRight 2s forwards; /* Adjust duration as needed */
  animation-delay: calc(var(--index) * 0.5s); /* Adjust delay as needed */
}

.left-container .subject {
  animation: slideInFromLeft 2s forwards; /* Adjust duration as needed */
  animation-delay: calc(var(--index) * 0.5s); /* Adjust delay as needed */
}

#clickMe { 
  background-image: url(../assets/media/general/light.png);
  width: 6vmax;
  height: 4vmax;
  background-size: 100% 100%;
  background-repeat: no-repeat;
  position: absolute;
  top: 3%;
  right: 2%;
  display: flex;
  justify-content: center;
  align-items: end;
  cursor: pointer;
  animation: pulse 2s infinite;
}

.clicked {
  animation: none !important;
}
.disappear {
  animation: fadeout 5s forwards !important;
}
@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.3);
  }
  100% {
    transform: scale(1);
  }
}

#clickMe p {
  position: relative;
  top: 3.2vh;
}


@keyframes fadeout {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}

#disappearing {
  opacity: 1; /* Start with opacity 0 for smoother transition */
  visibility: hidden;
  
}

.show {
  opacity: 1; /* Ensure opacity transition */
  position: absolute;
  visibility: visible !important;
  top: 5vh;
  right: 7vw;
  border: 2px solid #023E8A;
  padding: 0.5vw;
  width: 8vw;
  border-radius: 20vw;
  animation: fadeout 5s forwards;
}


.green {
  background-color: rgba(111, 222, 111, 0.543);
  color:#fff;
}

#yalla-next {
  width: 9vmax;
  height: 10vmax;
  position: absolute;
  bottom: 5%;
  left: 5%;
  background-image: url(../assets/media/general/yalla-next.png);
  background-size: 100% 100%;
  background-repeat: no-repeat;
  cursor: pointer;
  animation: pulse-smaller 1.25s infinite;
}

@keyframes pulse-smaller {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.035);
  }
  100% {
    transform: scale(1);
  }
}
</style>
