<template>
  <div id="advanced">
    <div class="back-home" @click="onSwitchPage"></div>
    <div class="title">{{ slidesInfo[curSlide].title }}</div>
    <div :class="{ text: true }" v-html="slidesInfo[curSlide].text"> </div>
    <div class="little">במידה והניסיון חיובי, מצוין!</div>

    <div v-for="(title, index) in titles" :key="title" @click="toggleContainer(index)" :class="[`title-${index}`, 'titles', { 'float': true }]">
      {{ title }}
    </div>

    <div v-for="(text, index) in texts" :key="text" :class="[`text-${index}`, 'texts', { 'show': activeIndexes.includes(index) }]">
      {{ text }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'advanced',
  props: ['componentName'],
  data() {
    return {
      curSlide: '1',
      titles: ['ניסיון חיובי', 'ניסיון שלילי'],
      texts: ['עלינו לתאם איתו ציפיות על מנת שלא יתאכזב', 'עלינו לנהל שיחה עם הנחנך כדי להסביר לו שמטרת התהליך היא חיובית ועבורו בלבד'],
      slidesInfo: {
        '1': {
          title: 'ניסיון קודם בתהליך חניכה',
          text: 'עלינו כחונכים להבין האם הנחנך שלנו בעל ניסיון קודם בתהליך החניכה.',
        },
      },
      activeIndexes: [],
    };
  },
  methods: {
    onSwitchPage() {
      this.$emit("add-green", this.componentName);
    },
    toggleContainer(index) {
      const idx = this.activeIndexes.indexOf(index);
      if (idx > -1) {
        this.activeIndexes.splice(idx, 1);
      } else {
        this.activeIndexes.push(index);
      }
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
  top: 18rem;
  font-size: 2rem;
  width: 60vw;
}

.little {
  top: 21rem;
  left: 50%;
  transform: translateX(-50%);
  position: absolute;
  font-size: 1.5rem;
  color: rgb(241, 108, 89);
}

.titles {
  font-size: 2.2rem;
  font-family: 'Heebo-bold';
  color: #023E8A;
  cursor: pointer;
  position: absolute;
  animation: float 4s ease-in-out infinite;
}

.title-0 {
  top: 45vh;
  right: 32vw;
}

.title-1 {
  top: 45vh;
  left: 32vw;
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

.texts {
  background-color: white;
  border-radius: 25px;
  padding: 1vw;
  font-size: 1.5rem;
  width: 15vw;
  position: absolute;
  top: 52vh;
  opacity: 0;
  transition: all 1.5s ease;
}

.texts.show {
  opacity: 1;
}

.text-0 {
  right: 28.5vw;
  transform: translateX(100%);
}

.text-0.show {
  transform: translateX(0);
}

.text-1 {
  left: 28.5vw;
  transform: translateX(-100%);
}

.text-1.show {
  transform: translateX(0);
}
</style>
