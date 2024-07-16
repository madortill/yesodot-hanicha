<template>
  <div id="introduction">
    <navbar :titleIndex="0" @switch-page="switchPage"></navbar>

    <div class="titles">{{ slidesInfo[curSlide].title }}</div>

    <div v-if="curSlide === '1' && !didVisit" id="clickMe" @click="showInfo">
      <p>לחצו עליי</p>
    </div>

    <div v-if="curSlide === '1'" id="disappearingMsg"> עברו על הטקסט עם העכבר ותראו מה יקרה </div>
    <div v-if="curSlide === '1'" class="text" v-html="formattedText"></div>
    <div v-if="showImage && curSlide === '1' && !didVisit" id="grandma"></div>
    <div v-if="didVisit && curSlide === '1'" id="grandma" class="no-animation"></div>

    <div v-else-if="curSlide === '2'" class="text1">
      <div v-for="(item, index) in slidesInfo[curSlide].text" :key="index" class="circle"
           @mouseover="circleHovered(index)" @mouseleave="circleLeft(index)"
           :style="{ backgroundColor: circleColors[index] }">
        {{ item }}
      </div>
    </div>

    <div v-else-if="curSlide === '3'" class="flip-card">
      <div class="flip-card-inner">
        <div>
          <img 
            src="../assets/media/introduction/target-front.png" 
            alt="target-front"
            class="target-front"
          />
        </div>
        <div class="flip-card-back">
          <img 
            src="../assets/media/introduction/target-back.png" 
            alt="target-back"
            class="target-front"
          />
        </div>
      </div>
    </div>

    <div v-show="curSlide === '4'">
      <div
        v-for="(value, key) in slide3Info"
        :key="key"
        :id="key"
        :class="{ 'container': key !== 'subtitle' }"
        @click="key !== 'subtitle' ? checkIfCorrect(key) : null"
        v-html="value"
      ></div>
  </div>

    <button v-if="curSlide !== '4'" class="button next" @click="nextTitle">המשך</button>
    <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
    <div id="yalla-next" v-if="curSlide === '4' && didClick" @click="nextPage"></div>
    <div class="message" v-if="curSlide === '4' && didClick"> {{ message }} </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
export default {
  name: "introduction",
  props: ['whereBeen'],
  data() {
    return {
      curSlide: '1',
      keyWords: ['התפתחות', 'קשר מתמשך', 'מסייע בהנחייתו'],
      showImage: false,
      array2Slide: ['תחומי החניכה', 'מוקד הלמידה - ביצועי הנחנך', 'ביצוע מלווה בעיבוד משותף', 'קשר בריא ומתמשך בין החונך לנחנך'],
      circleColors: ['#48CAE4', '#90E0EF', '#ADE8F4', '#CAF0F8'],
      slide3Info: {
        'subtitle' : 'לחצו על אחת האופציות וגלו מה התשובה הנכונה',
        'first' : '<div style="font-weight: bold; font-size: 2.4rem;">כן!</div> תהליך חניכה טוב הוא תהליך חניכה שמסתיים!<br><br> הסוף תלוי במידת<br> העצמאות שאליה הגיע הנחנך בביצועיו<br>',
        'second' : '<div style="font-weight: bold; font-size: 2.4rem;">לא!</div> תהליך חניכה אף פעם לא מסתיים!<br><br> תמיד יש לאן לשאוף ולהשתפר, לכן התליך הוא בלתי נגמר'
      },
      didVisit: false,
      didClick: false,
      message: null,
      slidesInfo: {
        '1': {
          title: 'מהי חניכה?',
          text: 'תהליך למידה אשר מטרתו התפתחות אישית ומתבסס על קשר מתמשך, שבו אדם מנוסה או בעל ידע רב יותר מסייע בהנחייתו של אדם בעל ידע או ניסיון מצומצמים יותר.'
        },
        '2': {
          title: 'עקרונות החניכה',
          text: []  
        },
        '3': {
          title: '',
          text: ''
        },
        '4': {
          title: 'האם לתהליך החניכה יש נקודת סיום?',
          text: {}
        }
      }
    }
  },
  created() {
    // Assign array2Slide to text for slide 2 after array2Slide is defined
    this.slidesInfo['2'].text = this.array2Slide;
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
    Navbar
  },
  mounted() {
    document.addEventListener('mouseover', this.keywordHovered);
  },
  methods: {
    switchPage(index) {
        if (this.whereBeen.includes(index)) {
          this.$emit('switch-screen', index);
        }
      },
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
  showInfo() {
    document.getElementById("clickMe").classList.add("clicked");
    document.getElementById("disappearingMsg").classList.add("showMsg");
    document.getElementById("clickMe").classList.add("disappear");
  },
  circleHovered(index) {
    const circles = document.querySelectorAll('.circle');
    circles[index].classList.add('circle-hovered');
  },
  circleLeft(index) {
    const circles = document.querySelectorAll('.circle');
    circles[index].classList.remove('circle-hovered');
  },
  makeHighlight() {
    document.removeEventListener('mouseover', this.keywordHovered);
    let keywordElements = document.querySelectorAll('.keyword');
    keywordElements.forEach((element) => { 
      console.log(element);
      element.style.fontSize = '2.4rem';
      element.style.fontWeight = 'bold';
      element.style.color = '#023E8A';
    });
  }, 
  checkIfCorrect(key) {
    this.didClick = true;
    document.getElementById("first").classList.add("clicked");
    document.getElementById("second").classList.add("clicked");
    if (key === "first") {
      document.getElementById("first").classList.add("correct");
      document.getElementById("second").classList.remove("incorrect");
      this.message = "כל הכבוד!"
      document.getElementById("first").removeEventListener("click", this.checkIfCorrect);
      document.getElementById("second").removeEventListener("click", this.checkIfCorrect);
    } else {
      document.getElementById("first").classList.remove("correct");
      document.getElementById("second").classList.add("incorrect");
      this.message = "לא נורא, נסה שוב"
    }
  },
  
  nextPage() {
    this.$emit("switch-screen", 3);
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
  animation: fadeout 5s forwards !important;
}

@keyframes pulse {
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

.text1 {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 20rem;
  font-size: 2rem;
  color: #03045E;
  width: 100vw;
  display: flex;
  justify-content: center;
}

.circle {
  display: flex;
  margin-left: -1.5vw;
  align-content: center;
  border-radius: 100%;  /* Makes the element circular */
  width: 14vw;
  height: 14vw;
  padding: 20px;  /* Adjust padding as needed */
  display: inline-block;  /* Ensures the element takes the shape of a circle */
  text-align: center;  /* Centers text inside the circle */
  transition: transform 0.3s ease, border-color 0.3s ease;  /* Smooth transition */
}

.circle-hovered {
  transform: scale(1.3);  /* Scale up on hover */
  cursor: pointer;  /* Change cursor on hover */
  align-items: center;
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

.target-front {
  position: absolute;
  top: 10vh;
  left: 50%;
  transform: translateX(-50%);
  width: 30vw;
}

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
  transition: transform 0.6s;
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
  top: 0.65vh;
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
}

</style>
