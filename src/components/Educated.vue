<template>
    <div id="educated">
      <navbar :titleIndex="3" @switch-page="switchPage"></navbar>
      <div class="title">{{ slidesInfo[curSlide].title }}</div>
      
      <div v-if="curSlide === '1'" class="pictures-container">
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
  
      <!-- <button v-if="curSlide !== '3'" class="button next" @click="nextTitle">המשך</button> -->
      <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
    </div>
  </template>
  
  <script>
 import Navbar from './Navbar.vue';

export default {
  name: "educated",
  props: ['whereBeen'],
  components: {
    Navbar,
  },
  emits: ['switch-screen', 'switch-page'],
  data() {
    return {
      slidesInfo: {
        '1': {
          'title': 'בתור חונכים, עלינו לנתח ולאפיין שני היבטים של הנחנך',
          'text': ''
        },
        '2': {
          'title': '',
          'text': ''
        },
        '3': {
          'title': '',
          'text': ''
        },
      },
      curSlide: '1',
    };
  },
  methods: {
    nextPage() {
      this.$emit("switch-screen", 7);
    },
    switchPage(index) {
      if (this.whereBeen.includes(index)) {
        this.$emit('switch-screen', index);
      }
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
    showSubtitles() {
      this.showingSubtitles = true;
    }
  },
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
  width: 60vw; /* Increased width */
  justify-content: space-around;
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
  transition: transform 2s; /* Flip duration */
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
  font-family: 'Heebo-bold';
  font-size: 2rem;
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
</style>
