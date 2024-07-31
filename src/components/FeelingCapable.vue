<template>
    <div id="feeling-capable">
      <div class="back-home" @click="onSwitchPage"></div>
      <div class="title"> {{ slidesInfo[curSlide].title }}</div>
      <div :class="{ text: true, higher :true }" v-html="slidesInfo[curSlide].text"> </div>

      <div v-if="curSlide === '2'" class="red">כיצד עושים את זה?</div>
      <div v-if="curSlide === '1'"> 
        <img class="low" src="../assets/media/educated/low.svg"/>
              <div class="subject2" @click="openMeOnce">נמוכה מדי</div>
              <div class="low-container">
                <div v-show="showMeForLow" class="info-container">
                  <div v-for="item in arrayInfoLow" :key="item">
                    {{ item }}
                  </div>
                </div>
              </div>

              <img class="high" src="../assets/media/educated/high.svg"/>
              <div class="subject1" @click="openMeAlways">גבוהה מדי</div>
              <div class="high-container">
                <div v-show="showMeForHigh" class="info-container">
                  <div v-for="item in arrayInfoHigh" :key="item">
                    {{ item }}
                  </div>
                </div>
              </div>
      </div>

      <div v-else>
        <removed-circles></removed-circles>
      </div>
      <button v-if="curSlide !== '2'" class="button next" @click="nextTitle">המשך</button>
      <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
    </div>
  </template>
  
  
  <script>
import RemovedCircles from './RemovedCircles.vue';


  export default {
      name: 'feeling-capable',
      props: ['componentName'],
      data() {
          return {
            curSlide: '1',
            arrayInfoLow: ['הנחנך עלול לחוש פחד קבוע מכישלון', 'לעסוק בתוצאות והשלכות', 'לאבד ריכוז במשימה', 'איך אנחנו כחונכים יכולים לעזור במצב כזה?'],
            arrayInfoHigh: ['הנחנך עלול לפתח שאננות', 'זלזול במשימה', 'אדישות וזלזול בחונך', 'וירידה באיכות ביצוע המשימה'],
            showMeForLow: false,
            showMeForHigh: false,
            slidesInfo: {
              '1' : {
                title: 'תחושת מסוגלות',
                text: 'אמונה של אדם לגבי יכולתו לבצע משימה שתביא לתוצאה מסוימת.<br> תחושת המסוגלות קובעת את מידת ההצלחה'
              },
              '2' : {
                title: 'פיתוח תחושת מסוגלות',
                text: 'עלינו כחונכים לספק תמונת מצב אמיתי לגבי היכולת של הנחנך ולהעלות את תחושת המסוגלות שלו'
              }
            }
          };
      },
      components: {
            RemovedCircles
      },
      methods: {
        onSwitchPage() {
          this.$emit("add-green", this.componentName);
        },
        nextTitle() {
          this.didVisit = true;
          this.showImage = true;
          let slideNum = Number(this.curSlide);
          slideNum++;
          this.curSlide = String(slideNum);
        },
        lastTitle() {
          let slideNum = Number(this.curSlide);
          slideNum--;
          this.curSlide = String(slideNum);
          this.showImage = this.didVisit;
        },
        openMeOnce() {
          this.showMeForLow = true;
        },
        openMeAlways() {
          this.showMeForHigh= true;
        },
      },
  };
  </script>
  
  
  <style scoped>
 .back-home {
      background-image: url(../assets/media/educated/go-home.png);
      width: 6vmax;
      height: 5.5vmax;
      background-size: 100% 100%;
      background-repeat: no-repeat;
      position: absolute;
      top: 5%;
      right: 2%;
      cursor: pointer;
      animation: pulse 2s infinite;
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
    font-size: 1.6rem;
    width: 60vw;
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
  height: 34vh;
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

.low-container {
  position: absolute;
  top: 48vh;
  left: 27vw;
}

.high-container {
  position: absolute;
  top: 48vh;
  right: 26vw;
}

.subject1 {
  font-family: "Heebo-bold";
  font-size: 3rem;
  color:#03045E;
  position: absolute;
  top: 40vh;
  right: 31vw;
  cursor: pointer;
}

.subject2 {
  font-family: "Heebo-bold";
  font-size: 3rem;
  color:#03045E;
  position: absolute;
  top: 40vh;
  left: 31.5vw;
  cursor: pointer;
}

.higher {
  position: absolute;
  top: 28vh;
  font-size: 1.8rem;
}

 .low, .high {
  width: 8vw;
  position: absolute;
  top: 35vh;
 }

 .low {
  left: 23vw;
 }
 
 .high {
  right: 23vw;
 }

 .red {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 32vh;
  font-size: 1.4rem;
  color: rgb(241, 108, 89);
 }

  </style>
  