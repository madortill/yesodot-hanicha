<template>
    <div id="summery">
      <div class="title"> {{ slidesInfo[curSlide].title }}</div>
      <div :class="{ text: true }" v-html="slidesInfo[curSlide].text"> </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "summery",
    data() {
      return {
        curSlide: '1',
           slidesInfo: {
          '1' : {
            title: 'סיכום',
            text: 'כל הכבוד, סיימת את הלומדה!'
           },
        }
      };
    },
    methods: {

    }
  };
  </script>
  
  <style scoped>
  #summery {
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
  
    
  
  </style>
  