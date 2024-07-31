<template>
  <div id="app">
     <navbar v-if="page > 0" :componentName="componentOrder[page]" @go-to-page="goToPage" :whereBeen="whereBeen"></navbar>
      <img id="icon-bahadim" src="@/assets/media/general/mifkada-logo.png" alt="bahadim"/>
      <img id="icon-til" src="@/assets/media/general/madortill.png" alt="till"/>
    <KeepAlive>
        <component :is="componentOrder[page]" @switch-screen="switchPage" :wherePulse="wherePulse"></component>
    </KeepAlive>

  </div>
</template>


<script>
import StartScreen from './components/StartScreen.vue';
import Introduction from '@/components/Introduction.vue';
import Triangle from './components/Triangle.vue'
import Event from './components/Event.vue'
import Educated from './components/Educated.vue';
import Educator from './components/Educator.vue';
import Summery from './components/Summery.vue';
import Navbar from './components/Navbar.vue';
import { KeepAlive } from 'vue';

export default {
    name: 'app',
    data() {
        return {
            page: 0,
            // page: 5,
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
                "educator", 
                "summery"
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
        Summery
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
