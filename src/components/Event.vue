<template>
    <div id="event">
      <navbar :titleIndex="2" @switch-page="switchPage"></navbar>
      <div class="title"> {{ slidesInfo[curSlide].title }}</div>
      <div :class="{ text: true, right: curSlide === '1', subtext: curSlide === '2', info: curSlide === '4' ||  curSlide === '5'}" v-html="slidesInfo[curSlide].text"> </div>

      <div v-if="curSlide === '1'">
        <img 
          src="../assets/media/event/heart.png" 
          alt="heart"
          class="heart" 
          @click="changeMe"/>

          <img v-for="i in 3" :key="i" :class="{ [`arrow-black-${i}`]: true, arrow: true }" src="../assets/media/event/arrow1.svg"/>
          <div v-for="(title, index) in array" :key="index" :class="['titles', `title-${index}`]"> {{ title }} </div>
          <div class="subtitle">תראו ללב קצת אהבה ולחצו עליו</div>

          <div class="container" v-show="showWindow">
              <div class="close" @click="changeMe">x</div>
              <div class="title inner">סוגי ביצועים</div>
              <div class="types-subtitle">עברו עם העכבר מעל הסוגים השונים כדי ללמוד עליהם</div>
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

              <div>
                <div v-show="showMeForOnce || showMeForAlways" class="place">
                  <div v-for="item in arraySubjects" :key="item" class="title-table">
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

      <div v-else-if="curSlide === '3'"> 
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

      <div v-else-if="curSlide === '4'" class="hanicha-container">
        <div v-for="(item, index) in arrayOfHanicha" :key="index" class="text-container" :style="{ backgroundColor: textColors[index] }">
          {{ item }}
        </div>
      </div>

      <div v-else class="wrapper-q">
        <div
          v-for="(value, key) in slide5Info"
          :id="key"
          :key="key"
          :class="{ 'container-q': true} "
          @click= "!didClick2 ? checkIfCorrect(key) : null"
        >
          {{ value }}
        </div>
      </div>
      <div id="yalla-next" v-if="curSlide === '5' && didClick2" @click="nextPage"></div>
      <div class="msg" v-if="curSlide === '5'"> {{ message }} </div>


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
       textColors: ['#CAF0F8','#ADE8F4', '#90E0EF', '#48CAE4', '#00B4D8'],
       arrayAgo: ["משוב", "עיבוד", "תצפית", "תדריך", "הכנה עצמית"],
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
          text: 'אלו השלבים של חניכה על תפקיד:'
        },
        '5': {
          title:'לפניכם סיטואציה, בחרו בתשובה המתאימה',
          text: 'סמלת הקורס לימדה את יובל (המ"כית החדשה) את תוכן השיעור "פירוק והרכבה". <br>באיזה סוג של חניכה מדובר?'
        }
      },
      typesOfOnce: {
        'מוטורי' : 'מיומנות אוטומטית (תפעול נשק)',
        'קוגנטיבי' : 'מיומנות קבלת החלטות לאור שיקולים וניתוח מצבים (הדרכה בכיתה, עריכת ראיון)',
        'רגשי' : 'היבט ערכי של הביצוע (הערכים הנדרשים להצלחה)'
      },
      arrayInfoOnce: ['זמן קצר - ימים עד שבועות', 'ביצוע בודד בעל גורם משפיע אחד', 'מומחה תוכן לביצוע', 'חשובה אך לא הכרחית'],
      arrayInfoAlways: ['זמן ארוך יחסית - שבועות עד שנים', 'מספר ביצועים בעלי גורמים משפיעים', 'לא תמיד צריך מומחה תוכן לכל ביצוע', 'קריטית והכרחית'],
      arraySubjects: ['משך החניכה','מורכבות החניכה','מומחיות החונך','תקשורת בין החונך לנחנך'],
      showMeForOnce: false,
      showMeForAlways: false,
      arrayOfHanicha: ['ניתוח מרכיבי תפקיד ומאפייני הנחנך', 'בניית תכנית חניכה - מטרות, אירועים, זמנים', 'שיחת פתיחה - יצירת חוזה ותיאום ציפיות', 'ניהול האירועים בעזרת מעגלי חניכה קרובים ורחוקים','מפגשי חניכה תקופתיים'],
      slide5Info: {
        'hello1' : 'חניכה על ביצוע',
        'hello2' : 'חניכה על תפקיד'
      },
      didClick2: false,
      message: ""
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
      },
      getCircleClass(index) {
      return "circle" + index;
      },
      getArrowClass(index) {
        return "arrow" + index;
      },
      checkIfCorrect(key) {
        document.getElementById("hello1").classList.add("clicked");
        document.getElementById("hello2").classList.add("clicked");
        if (key === "hello1") {
          this.didClick2 = true;
          document.getElementById("hello1").classList.add("correct");
          document.getElementById("hello2").classList.remove("incorrect");
          this.message = "כל הכבוד!"
          document.getElementById("hello1").removeEventListener("click", this.checkIfCorrect);
          document.getElementById("hello2").removeEventListener("click", this.checkIfCorrect);
        } else {
          document.getElementById("hello1").classList.remove("correct");
          document.getElementById("hello2").classList.add("incorrect");
          this.message = "לא נורא, נסה שוב"
        }
      },
      },
  computed: {
    showButton() {
      return this.curSlide !== '5' && (this.curSlide === '1' ? this.didClick && !this.showWindow : true);
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
    left: 14vw;
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

.types-subtitle {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 13vh;
  font-size: 1.4rem;
  color:rgb(241, 108, 89);
}


.arrow-black-1 {
  position: absolute;
  bottom: 30vh;
  left: 42vw;
  rotate: 120deg;
}

.arrow-black-2 {
  position: absolute;
  left: 21vw;
  bottom: 23vh;
  rotate: 290deg;
}
.arrow-black-3 {
  position: absolute;
  left: 20vw;
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
  left: 11vw;
  bottom: 24vh;
}

.title-1 {
  position: absolute;
  left: 14vw;
  top: 40vh;
}

.title-2 {
  position: absolute;
  right: 45vw;
  bottom: 30vh;
}

.titles {
   font-size: 2.2rem;
   color: #03045E;
}

.subtitle {
  position: absolute;
  left: 25.5vw;
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

.wrapper {
  position: relative;
  top: 55%;
  left: -50%;
  transform: translate(50%, -50%);
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

.place {
  position: absolute;
  left: 46.5vw;
  top: 42vh;
}

.title-table {
  background-color: #8cacec;
  margin-top: 2vh;
  border-radius: 15px;
  padding: 0.5vw;
  font-size: 1.2rem;
  width: 6vw;
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

.hanicha-container {
  position: absolute;
  bottom: 9vh;
  left: 50%;
  transform: translateX(-50%);
}

.text-container {
  width: 20vw;
  font-size: 1.5rem;
  margin-top: 1vh;
  padding: 1vw;
  border-radius: 20px;
  cursor: auto;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.text-container:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  cursor: auto;
}


.info {
  top: 28vh;
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

.correct {
  background-color: rgba(111, 222, 111, 0.543);
  border: none !important;
}

.incorrect {
  background-color: rgba(241, 109, 89, 0.824);
  border: none !important;
}

.clicked {
  animation: none !important;
}


.container-q {
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


.wrapper-q {
  position: absolute;
  top: 63%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  width: 50vw;
}

.msg {
  position: absolute;
  font-size: 3rem;
  font-family: "Heebo-bold";
  left: 50%;
  transform: translateX(-50%);
  bottom: 9vh;
  color: #023E8A;
}
  </style>
  