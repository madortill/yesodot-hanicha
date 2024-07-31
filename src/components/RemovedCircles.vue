<template>
    <div id="removed-circles">
      <div class="text">
        <div v-for="(item, index) in slidesInfo[curSlide].text" :key="index" class="circle"
             @mouseover="circleHovered(index)" @mouseleave="circleLeft(index)"
             :style="{ backgroundColor: circleColors[index] }">
          {{ item }}
        </div>
      </div>
    </div>
  </template>
  
  <script>

  export default {
    name: "removed-circles",
    props: [''],
    data() {
      return {
        array2Slide: ['הטלת משימות בהתאם ליכולת', 'למידה דרך תצפיות על אחרים', 'שימוש בסיפורים אישיים ודוגמאות מהעבר', 'ביטול "תפיסת המקריות" אצל הנחנך', 'איסוף הצלחות קטנות וחלקיות', 'לגיטימציה לטעויות ואי הסכמה'],
        circleColors: ['#0077B6','#00B4D8','#48CAE4', '#90E0EF', '#ADE8F4', '#CAF0F8'],
        curSlide: '2',
        slidesInfo: {
          '2': {
            title: 'עקרונות החניכה',
            text: []  
        }
      }
     }
    },
    created() {
      // Assign array2Slide to text for slide 2 after array2Slide is defined
      this.slidesInfo['2'].text = this.array2Slide;
    },
    methods: {
    circleHovered(index) {
      const circles = document.querySelectorAll('.circle');
      circles[index].classList.add('circle-hovered');
    },
    circleLeft(index) {
      const circles = document.querySelectorAll('.circle');
      circles[index].classList.remove('circle-hovered');
    }
  }
}
  </script>
  
  <style scoped>
  #removed-circles {
    text-align: center;
  }
  
  
  .text {
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
  

  </style>
  