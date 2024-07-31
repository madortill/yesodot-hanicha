<template>
    <div id="learning-habbits">
      <div class="back-home" @click="onSwitchPage"></div>
      <div class="title"> {{ slidesInfo[curSlide].title }}</div>
      <div :class="{ text: true }" v-html="slidesInfo[curSlide].text"> </div>
      <button v-if="curSlide !== '2'" class="button next" @click="nextTitle">המשך</button>
      <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
    </div>
  </template>
  
  
  <script>


  export default {
      name: 'learning-habbits',
      props: ['componentName'],
      data() {
          return {
            curSlide: '1',
            slidesInfo: {
              '1' : {
                title: 'הרגלי למידה',
                text: ''
              },
              '2' : {
                title: '',
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
    top: 20rem;
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

  </style>
  