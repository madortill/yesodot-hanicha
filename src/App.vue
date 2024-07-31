<template>
  <div id="app">
     <navbar v-if="page > 0" :componentName="componentOrder[page]" @go-to-page="goToPage" :whereBeen="whereBeen"></navbar>
      <img id="icon-bahadim" src="@/assets/media/general/mifkada-logo.png" alt="bahadim"/>
      <img id="icon-til" src="@/assets/media/general/madortill.png" alt="till"/>
    <KeepAlive>
        <component :is="componentOrder[page]" @switch-screen="switchPage" :wherePulse="wherePulse"></component>
    </KeepAlive>

      <!-- <start-screen v-show="page === 1" @switch-screen="switchPage"></start-screen>
      <introduction v-show="page === 2" @switch-screen="switchPage"></introduction>
      <triangle v-show="page === 3" @switch-screen="switchPage" :wherePulse="wherePulse"></triangle>
      <event v-show="page === 4" @switch-screen="switchPage"></event>
      <triangle v-show="page === 5" @switch-screen="switchPage" :wherePulse="wherePulse"></triangle>
      <educated v-show="page === 6" @switch-screen="switchPage"></educated>
      <triangle v-show="page === 7" @switch-screen="switchPage" :wherePulse="wherePulse"></triangle>
      <educator  v-show="page === 8" @switch-screen="switchPage"></educator> -->
  </div>
</template>


<script>
import StartScreen from './components/StartScreen.vue';
import Introduction from '@/components/Introduction.vue';
import Triangle from './components/Triangle.vue'
import Event from './components/Event.vue'
import Educated from './components/Educated.vue';
import Educator from './components/Educator.vue';
import Navbar from './components/Navbar.vue';
import { KeepAlive } from 'vue';

export default {
    name: 'app',
    data() {
        return {
            page: 0,
            whereBeen: ["start-screen"],
            wherePulse: 'event',
            componentOrder: [
                "start-screen",
                "introduction",
                "triangle",
                "event",
                "triangle",
                "educated",
                "triangle",
                "educator"
            ]
        };
    },
    components: {
        Navbar,
        StartScreen,
        Introduction,
        Triangle,
        Event,
        Educated,
        Educator,
    },
    methods: {
        switchPage() {
            this.page++;
            
            if (!this.whereBeen.includes(this.componentOrder[this.page])) {
                this.whereBeen.push(this.componentOrder[this.page]);
            }
            if (this.page === 4) {
                this.wherePulse = 'educated';
            }
            if (this.page === 6) {
                this.wherePulse = 'educator';
            }
        },
        goToPage (name) {
            this.page = this.componentOrder.indexOf(name);
        }
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
