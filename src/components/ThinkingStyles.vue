<template>
  <div id="thinking-styles">
    <div class="back-home" @click="onSwitchPage"></div>
    <div class="title">{{ slidesInfo[curSlide].title }}</div>
    <div :class="{ text: true }" v-html="slidesInfo[curSlide].text"></div>

    <div class="flip-card-container">
      <div v-for="(card, index) in cards" :key="index" class="flip-card">
        <div class="flip-card-inner">
          <div class="flip-card-front">
            <img :src="card.image" alt="Card image" />
          </div>
          <div class="flip-card-back">
            <h1>{{ card.title }}</h1>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'thinking-styles',
  props: ['componentName'],
  data() {
    return {
      curSlide: '1',
      slidesInfo: {
        '1': {
          title: 'סגנונות חשיבה ולמידה',
          text: 'ישנם שלושה סוגים של סגנונות למידה עיקריים ולכל אדם יש סגנון שמתאים לו'
        }
      },
      cards: [
        { image: './educated/hearing.png', title: 'שמיעתי' },
        { image: './educated/touching.png', title: 'מוחשי' },
        { image: './educated/visual.png', title: 'ויזואלי' }
      ]
    };
  },
  methods: {
    onSwitchPage() {
      this.$emit("add-green", this.componentName);
    }
  }
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

.flip-card-container {
  display: flex;
  justify-content: space-around;
  margin-top: 20rem;
}

.flip-card {
  perspective: 1000px;
  margin-left: 1vw;
  width: 17vw; /* Adjusted to match image size */
  height: 17vw; /* Adjusted to match image size */
  border-radius: 50%;
}

.flip-card-inner {
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
  position: relative;
  border-radius: 50%;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 50%;
}

.flip-card-front {
  background-color: #bbb;
}

.flip-card-front img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
}

.flip-card-back {
  background-color: rgb(83, 83, 141);
  color: white;
  transform: rotateY(180deg);
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
