<template>
  <div id="introduction">
    <div class="titles">{{ slidesInfo[curSlide].title }}</div>


    <div v-if="curSlide === '1' && !didClick1" id="clickMe" @click="showInfo">
      <p>לחצו עליי</p>
    </div>

    <div v-if="curSlide === '1'" id="disappearingMsg"> עברו על הטקסט עם העכבר ותראו מה יקרה </div>
    <div v-if="curSlide === '1'" class="text" v-html="formattedText"></div>
    <div v-if="showImage && curSlide === '1' && !didVisit" id="grandma"></div>
    <div v-if="didVisit && curSlide === '1'" id="grandma" class="no-animation"></div>

    <!-- <removed-circles></removed-circles> -->
    <div v-else-if="curSlide === '0'">
      <div class="circle-container">
            <div
              v-for="(item, index) in arrayAgo"
              :key="index"
              class="circle"
              :class="getCircleClass(index)"
            >
              {{ arrayAgo[index] }}
            </div>
          </div>
          <!-- the arrows -->
           <div>
              <img
              v-for="i in 5"
              :key="i"
              class="arrow"
              :class="getArrowClass(i)"
              src="../../src/assets/media/event/arrow.svg"
            />
           </div>
         
    </div> 

    <div v-else-if="curSlide === '2'" >
      <flip-card 
        :folder="folderName"
        :frontName="frontName"
        :backName="backName"
        >
      </flip-card>
    </div>

    <div v-show="curSlide === '3'">
      <div
        v-for="(value, key) in slide3Info"
        :key="key"
        :id="key"
        :class="{ 'container': key !== 'subtitle' }"
        @click="key !== 'subtitle' && !didClick2 ? checkIfCorrect(key) : null"
        v-html="value"
      ></div>
  </div>

    <button v-if="curSlide !== '3'" class="button next" @click="nextTitle">המשך</button>
    <button v-if="curSlide !== '0'" class="button back" @click="lastTitle">חזור</button>
    <div id="yalla-next" v-if="curSlide === '3' && didClick2" @click="nextPage"></div>
    <div class="message" v-if="curSlide === '3'"> {{ message }} </div>
  </div>
</template>

<script>

import RemovedCircles from './RemovedCircles.vue';
import FlipCard from './FlipCard.vue';
export default {
  name: "introduction",
  data() {
    return {
      curSlide: '0',
      frontName: "target-front",
      backName: "target-back",
      folderName: "introduction",
      keyWords: ['למידה', 'קשר מתמשך', 'מסייע ומנחה'],
      arrayAgo: ["משוב", "עיבוד", "תצפית", "תדריך", "הכנה עצמית"],
      showImage: false,
      slide3Info: {
        'subtitle' : 'בחרו בתשובה הנכונה',
        'first' : '<div style="font-weight: bold; font-size: 2.4rem;">כן!</div> תהליך חניכה טוב הוא תהליך חניכה שמסתיים!<br><br> הסוף תלוי במידת<br> העצמאות שאליה הגיע הנחנך בביצועיו<br>',
        'second' : '<div style="font-weight: bold; font-size: 2.4rem;">לא!</div> תהליך חניכה אף פעם לא מסתיים!<br><br> תמיד יש לאן לשאוף ולהשתפר, לכן התליך הוא בלתי נגמר'
      },
      didVisit: false,
      didClick1: false,
      didClick2: false,
      message: null,
      slidesInfo: {
        '0': {
          title: 'ברוכים הבאים למעגל החניכה',
          text: ''
        },
        '1': {
          title: 'מהי חניכה?',
          text: 'תהליך למידה שמתבסס על קשר מתמשך, בו אדם מנוסה מסייע ומנחה אדם בעל ידע מצומצם יותר.'
        },
        '2': {
          title: '',
          text: ''
        },
        '3': {
          title: 'האם לתהליך החניכה יש נקודת סיום?',
          text: {}
        }
      }
    }
  },
  created() {
    this.slidesInfo['3'].text = this.slide3Info;
  },
  computed: {
    formattedText() {
      let text = this.slidesInfo[this.curSlide].text;
      if (Array.isArray(text)) {
        text = text.join(', ');  // Join array items with commas if text is an array
      }
        this.keyWords.forEach(word => {
        const re = new RegExp(`(${word})`, 'g');
        text = text.replace(re, `<span class="keyword">$1</span>`);
      });
      if (this.didVisit) {
        this.makeHighlight();
        this.$nextTick(() => {
        this.makeHighlight();
      });
      }
      return text;
    }
  },
  components: {
    RemovedCircles,
    FlipCard
  },
  mounted() {
    document.addEventListener('mouseover', this.keywordHovered);
  },
  methods: {
    
  keywordHovered(event) {
    if (event.target.classList.contains('keyword') && !this.showImage) {
      setTimeout(() => {
        this.showImage = true;
      }, 3000);
    }
    if (event.target.classList.contains('keyword')) {
      event.target.style.fontSize = '2.4rem';
      event.target.style.fontWeight = 'bold';
      event.target.style.color = '#023E8A';
    }
  },
  nextTitle() {
    let slideNum = Number(this.curSlide);
    slideNum++;
    this.curSlide = String(slideNum);
  },
  lastTitle() {
    this.didVisit = true;
    this.showImage = true;
    let slideNum = Number(this.curSlide);
    slideNum--;
    this.curSlide = String(slideNum);
    this.showImage = this.didVisit;
  },
  showInfo() {
    setTimeout( () => {
      this.didClick1=true;
    }, 5000);
    document.getElementById("clickMe").classList.add("clicked");
    document.getElementById("disappearingMsg").classList.add("showMsg");
    document.getElementById("clickMe").classList.add("disappear");
  },
  makeHighlight() {
    document.removeEventListener('mouseover', this.keywordHovered);
    let keywordElements = document.querySelectorAll('.keyword');
    keywordElements.forEach((element) => { 
      element.style.fontSize = '2.4rem';
      element.style.fontWeight = 'bold';
      element.style.color = '#023E8A';
    });
  }, 
  checkIfCorrect(key) {
    document.getElementById("first").classList.add("clicked");
    document.getElementById("second").classList.add("clicked");
    if (key === "first") {
      this.didClick2 = true;
      document.getElementById("first").classList.add("correct");
      document.getElementById("second").classList.remove("incorrect");
      this.message = "כל הכבוד!"
      document.getElementById("first").removeEventListener("click", this.checkIfCorrect);
      document.getElementById("second").removeEventListener("click", this.checkIfCorrect);
    } else {
      this.didClick = false;
      document.getElementById("first").classList.remove("correct");
      document.getElementById("second").classList.add("incorrect");
      this.message = "לא נורא, נסה שוב"
    }
  },
  getCircleClass(index) {
      return "circle" + index;
      },
      getArrowClass(index) {
        return "arrow" + index;
      },
  
  nextPage() {
    this.$emit("switch-screen");
  }
  }
}
</script>

<style scoped>
#introduction {
  text-align: center;
}

.titles {
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
.keyword {
  transition: font-size 1s, color 1s;
}

.keyword:hover,
.keyword.highlights {
  font-size: 2.4rem;  /* Adjust the size as desired */
  font-weight: bold;  /* Add other styles if needed */
  color: #023E8A;    /* Change color on hover */
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
  animation: fadeout 7s forwards !important;
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

#disappearingMsg {
  display: none;
}

@keyframes fadeout {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}

.showMsg {
  display: block !important;
  position: absolute;
  top: 5vh;
  right: 7vw;
  border: 2px solid #023E8A;
  padding: 0.5vw;
  width: 10vw;
  border-radius: 20vw;
  animation: fadeout 5s forwards;
}

#grandma {
  background-image: url(../assets/media/introduction/grandma.png);
  width: 33vmax;
  height: 14vmax;
  background-size: 100% 100%;
  background-repeat: no-repeat;
  animation: pulse1 2s forwards;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 18.5vh;
}

.no-animation {
  animation: none !important;
}

@keyframes pulse1 {
  0% {
    transform: translateX(-50%) scale(1);
  }
  50% {
    transform: translateX(-50%) scale(1.2);
  }
  100% {
    transform: translateX(-50%) scale(1);
  }
}

#subtitle {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 16rem;
  font-size: 1.4rem;
  color: rgb(241, 108, 89);
}

.container {
  font-size: 1.8rem;
  width: 20vw;
  height: 35vh;
  border: 2.5px solid #023E8A;
  color: #023E8A;
  border-radius: 5vmax;
  align-content: center;
  cursor: pointer;
  padding: 0.9vw;
  animation: pulse-smaller 2s infinite;
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

#first {
  position: absolute;
  top: 37vh;
  right: 26vw;
}

#second {
  position: absolute;
  top: 37vh;
  left: 26vw;
}

.correct {
  background-color: rgba(111, 222, 111, 0.543);
  border: none;
}

.incorrect {
  background-color: rgba(241, 109, 89, 0.824);
  border: none;
}

.clicked {
  animation: none !important;
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

.message {
  position: absolute;
  font-size: 3rem;
  font-family: "Heebo-bold";
  left: 50%;
  transform: translateX(-50%);
  bottom: 13vh;
  color: #023E8A;
}


.arrow {
  width: 4rem;
  position: absolute;
}

.arrow1 {
  top: 35%;
  right: 42%;
  transform: rotate(150deg);
}

.arrow2 {
  top: 35%;
  left: 42%;
  transform: rotate(100deg);
}

.arrow3 {
  bottom: 31%;
  left: 38%;
  transform: rotate(-10deg);
}

.arrow4 {
  bottom: 15%;
  left: 48%;
  transform: rotate(-60deg);
}

.arrow5 {
  bottom: 31%;
  right: 37%;
  transform: rotate(240deg);
}

.circle {
  width: 100%;
  height: 7rem;
  border-radius: 50%;
  text-align: center;
  color: white;
  font-size: 1.5rem;
  font-weight: 550;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1.6%;
  transition: all 0.3s ease;
  /* animation: floatAnimation 3s ease-in-out infinite; */
  box-shadow: 0 5px 7px rgba(0, 0, 0, 0.2);
  /* background-color: #eb5781; */
}

.circle:hover {
  box-shadow: 0 15px 9px rgba(0, 0, 0, 0.4);
  width: 8rem;
  height: 8rem;
  padding: 2%;
  /* cursor: pointer; */
}

.circle-container {
  position: absolute;
  top: 30%;
  left: 50%;
  transform: translateX(-50%);
  width: 40vw; /* Adjust the width to fit your design */
  height: 70%; /* Adjust the height to fit your design */
  margin: auto; /* Center the container */
  display: grid;
  grid-template-columns: repeat(7, 14.3%);
  grid-template-rows: repeat(5, 20%);
}

.circle0 {
  grid-column-start: 6;
  grid-row-start: 2;
  position: relative;
  background-color: #90E0EF;
}

.circle1 {
  grid-column-start: 5;
  grid-row-start: 4;
  background-color: #48CAE4;
}

.circle2 {
  grid-column-start: 3;
  grid-row-start: 4;
  background-color: #00B4D8;
}

.circle3 {
  grid-column-start: 2;
  grid-row-start: 2;
  background-color: #0096C7;
}

.circle4 {
  grid-column-start: 4;
  grid-row-start: 0;
  background-color: #0077B6;
}

</style>
