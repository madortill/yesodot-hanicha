<template>
  <div id="educator">
    <div class="title"> {{ slidesInfo[curSlide].title }}</div>
    <div :class="{ text: true }" v-html="slidesInfo[curSlide].text"> </div>

    <button v-if="curSlide !== '2'" class="button next" @click="nextTitle">המשך</button>
    <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
    <div id="yalla-next" v-if="curSlide === '2'" @click="nextPage"></div>
  </div>
</template>

<script>
export default {
  name: "educator",
  data() {
    return {
      curSlide: '1',
         slidesInfo: {
        '1' : {
          title: 'חונך',
          text: 'סרטון'
         },
        '2' : {
          title: 'אז מה התשובה הנכונה?',
          text: 'אין.<br> על מנת להיות חונכים מוצלחים עליכם להתאים את סוג החניכה לנחנך.<br> ברוב המקרים, חונך מכוון תוצאה יתאים  לחניכה על ביצוע בודד, בעוד שחונך מכוון תהליך יתאים לחניכה על תפקידץ ניתן גם לשלב בין השניים'
        }
      }
    };
  },
  methods: {
    nextPage() {
        this.$emit("switch-screen");
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
          this.showImage = this.didVisit;
        },
  }
};
</script>

<style scoped>
#educator {
  font-family: "Heebo";
  text-align: center;
  display: flex;
  justify-content: center;
  overflow-x: hidden;
  overflow-y: hidden;
}
.title {
  font-size: 4rem;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 11rem;
  font-family: "Heebo-bold";
  color: #0077b6;
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

</style>
