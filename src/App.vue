<template>
  <div id="app">
      <img id="icon-bahadim" src="@/assets/media/general/mifkada-logo.png" alt="bahadim"/>
      <img id="icon-til" src="@/assets/media/general/madortill.png" alt="till"/>
      <start-screen v-show="page === 1" @switch-screen="switchPage"></start-screen>
      <introduction v-show="page === 2" @switch-screen="switchPage" :whereBeen="whereBeen"></introduction>
      <triangle v-show="page === 3" @switch-screen="switchPage" :whereBeen="whereBeen" :wherePulse="wherePulse"></triangle>
      <event v-show="page === 4" @switch-screen="switchPage" :whereBeen="whereBeen"></event>
      <div v-show="page === 5" @switch-screen="switchPage" :whereBeen="whereBeen"></div>
      <div v-show="page === 6" @switch-screen="switchPage" :whereBeen="whereBeen"></div>
   
  </div>
</template>


<script>
import StartScreen from './components/StartScreen.vue';
import Introduction from '@/components/Introduction.vue';
import Triangle from './components/Triangle.vue'
import Event from './components/Event.vue'

export default {
    name: 'app',
    data() {
        return {
            // page: 1,
            page: 4,
            whereBeen: [2],
            wherePulse: 'event',
        };
    },
    components: {
        StartScreen,
        Introduction,
        Triangle,
        Event
    },
    methods: {
        switchPage(page) {
            this.page = page;
            if (!this.whereBeen.includes(page)) {
            this.whereBeen.push(page);

            if (this.whereBeen.includes(5)) {
                 this.wherePulse= 'educated';
            } 

            if (this.whereBeen.includes(6)) {
                this.wherePulse= 'educator';
            }
        }
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

#icon-bahadim {
    max-width: 100px;
    left: 0;
    top: 0;
    position: absolute;
    margin-top: 1%;
    margin-left: 1%;
    z-index: 3;
}

#icon-til {
    /* min-width: 20px; */
    max-height: 10%;
    max-width: 90px;
    position: absolute;
    bottom: 0;
    right: 0;
    margin-bottom: 1%;
    margin-right: 1%;
    z-index: 3;
}
</style>
