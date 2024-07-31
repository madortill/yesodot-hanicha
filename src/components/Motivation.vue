<template>
    <div id="motivation">
      <div class="back-home" @click="onSwitchPage"></div>
      <div class="title"> {{ slidesInfo[curSlide].title }}</div>
      <div :class="{ text: true }" v-html="slidesInfo[curSlide].text"> </div>

      <div v-if="curSlide === '1'">
          <div class="wrapper">
            <div v-for="(value, key) in typesOfOnce" :key="key" class="flip-card">
              <div class="flip-card-inner">
                <div class="flip-card-front">
                  {{ key }}
                </div>
                <div class="flip-card-back">
                  {{ value }}
                </div>
              </div>
            </div>
        </div>
      </div>

       <div v-else class="containerOfMotivation">
          <div v-for="item in motivationArray" :key="item" class="white-wrap">
          {{ item }}
          </div>
       </div>

      <button v-if="curSlide !== '2'" class="button next" @click="nextTitle">המשך</button>
      <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
    </div>
  </template>
  
  
  <script>


  export default {
      name: 'motivation',
      props: ['componentName'],
      data() {
          return {
            curSlide: '1',
            typesOfOnce: {
              'אוטונומיה' : 'התשוקה לשלוט בחיינו בעצמנו על ידי שליטה במשימות, זמן, שיטה וצוות.',
              'מומחיות' : 'הדחף האנושי להשתפר עוד ועוד במשהו שחשוב לנו',
              'תכלית' : 'זוהי השאיפה לעשות את מה שאנחנו עושים במסגרת משהו גדול יותר מעצמנו'
            },
            motivationArray: ['טיפוח מוטיבציה', 'מה מפתחים קודם?', 'הגדלת אחריות והצבת אתגרים', 'פיתוח מיומנות ותחושת המסוגלות'],
            slidesInfo: {
              '1' : {
                title: 'מוטיבציה',
                text: 'המוטביציה מורכבת משלושה תחומים:'
              },
              '2' : {
                title: 'יכולת מול מוטיבציה',
                text: ''
              }
            }
          };
      },
      components: {
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
    top: 17rem;
    font-size: 2rem;
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


.wrapper {
  position: absolute;
  top: 58%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  width: 60vw;
}

.flip-card {
  background-color: transparent;
  width: 17vw; /* Adjust width as needed */
  height: 17vw; /* Adjust height as needed */
  perspective: 1000px;
  border-radius: 50%; /* Add perspective to the container */
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  cursor: pointer;
 
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 5vmax;
  padding: 2vw; /* Adjust padding as needed */
  box-sizing: border-box; /* Ensure padding does not affect the total size */
}

.flip-card-front {
  background-color: #8cacec;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem; /* Adjust font size as needed */
  font-family: 'Heebo-bold';
}

.flip-card-back {
  background-color: #8cacec;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px; /* Adjust font size as needed */
  transform: rotateY(180deg);
}

.containerOfMotivation {
  position: absolute;
  top: 60%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* border: solid; */
  display: flex;
  flex-wrap: wrap;
  width: 32vw;
  height: 30vh;
}

.white-wrap{
  text-align: center;
  align-content: center;
  background-color: #fff;
  border-radius: 25px;
  padding: 1vw;
  font-size: 1.8rem;
  margin: 1vw;
  width: 12vw;
}
  </style>
  