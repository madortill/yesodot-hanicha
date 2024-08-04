<template>
  <div id="app">
    <button v-show = "page === 0" class = "aboutBtn" @click = "openAbout">i</button>
    <Transition v-show = "page === 0">
          <div v-show = "showAbout" class="div-about">
          <h3 class = "list-text-about">מפתחת ראשית:</h3>
            <p class = "list-text-about">טור' גילי גורדון</p>
            <h3 class = "list-text-about">גרפיקה:</h3>
            <p class = "list-text-about">טור' גילי גורדון</p>
            <h3 class = "list-text-about">רת"ח מו"פ:</h3>
            <p class = "list-text-about">רס"ל אביב אואנונו</p>
            <h3 class = "list-text-about">רמ"ד טי"ל:</h3>
            <p class = "list-text-about">רס"מ שלומי אוגרן</p>
            <h3 class = "list-text-about">גרסה:</h3>
            <p class = "list-text-about">אוגוסט 2024</p>
        </div>
      </Transition>
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
            showAbout: false,
            clickBtn: 0,
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
        },
        openAbout() {
            if (this.clickBtn % 2 === 0) {
                this.showAbout = true;
            } else {
                this.showAbout = false
            }
            this.clickBtn++;
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


.aboutBtn {
  position: absolute;
  border: none;
  color: white;
  font-size: 1.6rem;
  transition: background-color 0.3s ease;
  background-color: #02ade1;
  border-radius: 150px;
  width: 2%;
  height: 4%;
  cursor: pointer;
  left: 2.5%;
  top: 14%;

}

.aboutBtn:hover{
  background-color: #038eb9;
}
.div-about {
  position: absolute;
  width: 12%;
  left: 6%;
  top: 13%;
  background: #fff;
  border-radius: 1rem;
  box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
  text-align: center;
  z-index: 3;
}

.list-text-about {
  transition: background-color 0.5s ease;
  margin: 5%;
}
.list-text-about:hover {
  background-color: #dbdbdb;
}
</style>
