<template>
    <div id="introduction">
      <navbar :titleIndex="0"></navbar>
      <div v-if="curSlide === '1'" id="clickMe" @click="showInfo">
        <p>לחצו עליי</p>
      </div>
      <div v-if="curSlide === '1'" id="disappearingMsg"> עברו על הטקסט עם העכבר ותראו מה יקרה </div>
      <div  class="titles">{{ slidesInfo[curSlide].title }}</div>
      <div class="text" v-html="formattedText"></div>
      <div v-if="showImage && curSlide === '1'" class="grandma"></div>
      <button v-if="curSlide !== '4'" class="button next" @click="nextTitle">המשך</button>
      <button v-if="curSlide !== '1'" class="button back" @click="lastTitle">חזור</button>
    </div>
  </template>
  

  <script>
  import Navbar from '@/components/Navbar.vue';
  
  export default {
    name: "introduction",
    data() {
      return {
        curSlide: '1',
        slidesInfo: {
          '1' : {
              title: 'מהי חניכה?',
              text: 'תהליך למידה אשר מטרתו התפתחות אישית ומתבסס על קשר מתמשך, שבו אדם מנוסה או בעל ידע רב יותר מסייע בהנחייתו של אדם בעל ידע או ניסיון מצומצמים יותר.'
          },
          '2' : {
              title: 'עקרונות החניכה',
              text: ''
          },
          '3' : {
              title: '',
              text: ''
          },
          '4' : {
              title: 'האם תהליך החניכה מסתיים בכלל מתישהו?',
              text: ''
          }
       },
       keyWords: ['התפתחות', 'קשר מתמשך', 'מסייע בהנחייתו'],
       showImage: false,
      }
    },
    computed: {
      formattedText() {
        let text = this.slidesInfo[this.curSlide].text;
        this.keyWords.forEach(word => {
          const re = new RegExp(`(${word})`, 'g');
          text = text.replace(re, `<span class="keyword">$1</span>`);
        });
        return text;
      }
    },
    components: {
      Navbar
    },
    methods: {
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
      showInfo() {
          document.getElementById("clickMe").classList.add("clicked");
          document.getElementById("disappearingMsg").classList.add("showMsg");
          document.getElementById("clickMe").classList.add("disappear");
      }
    },
    mounted() {
      document.addEventListener('mouseover', this.keywordHovered);
    },
    beforeDestroy() {
      document.removeEventListener('mouseover', this.keywordHovered);
    },
    methods: {
      keywordHovered(event) {
        setTimeout( () => {
            this.showImage = true;
        }, 3000);
        if (event.target.classList.contains('keyword')) {
          event.target.style.fontSize = '2.4rem';  // Adjust the size as desired
          event.target.style.fontWeight = 'bold';  // Add other styles if needed
          event.target.style.color = '#023E8A';    // Change color on hover
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
      showInfo() {
        document.getElementById("clickMe").classList.add("clicked");
        document.getElementById("disappearingMsg").classList.add("showMsg");
        document.getElementById("clickMe").classList.add("disappear");
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
    transition: font-size 0.3s ease, color 0.3s ease;
  }
  
  .keyword:hover {
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
  
.grandma {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    bottom: 10vh;
    background-image: url(../assets/media/introduction/grandma.png);
    width: 44vmax;
    height: 20vmax;
    background-size: 100% 100%;
    background-repeat: no-repeat;
}

  </style>
  