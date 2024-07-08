<template>
  <div id="app">
      <!-- <img id="icon-bahadim" src="src/assets/media/general/bahadim-icon.png" alt="bahadim"/> -->
      <!-- <img id="icon-til" src="src/assets/media/general/til.png" alt="bahadim"/> -->
      <start-screen v-if="page === 1" @switch-screen="switchPage"></start-screen>
      <introduction v-if="page === 2" @switch-screen="switchPage"></introduction>
  </div>
</template>


<script>
import StartScreen from './components/StartScreen.vue';
import Introduction from './components/Introduction.vue';

export default {
    name: 'app',
    data() {
        return {
            page: 1,
        };
    },
    components: {
        StartScreen,
        Introduction,
    },
    methods: {
        switchPage(page) {
            this.page = page;
        },
    },
};
</script>


<style scoped>
@font-face {
    font-family: "Heebo-bold";
    src: url(./assets/fonts/heebo.extrabold.ttf);
}

@font-face {
    font-family: "Heebo";
    src: url(./assets/fonts/heebo.regular.ttf);
}

#app {
    direction: rtl;
    width: 100vw;
    height: 100vh;
    font-family: "Heebo";
    background-color: #ebebeb;
    overflow: hidden;
}

#icon-til {
    max-width: 125px;
    right: 0;
    bottom: 0;
    position: absolute;
    margin-top: 1%;
    margin-left: 1%;
    z-index: 3;
}

#icon-bahadim {
    max-width: 125px;
    left: 0;
    top: 0;
    position: absolute;
    margin-top: 1%;
    margin-left: 1%;
    z-index: 3;
}
</style>
