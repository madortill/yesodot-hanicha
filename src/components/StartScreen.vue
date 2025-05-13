<template>
    <div id="start-screen">
        <div class="title" v-if="!showInstructions">
            <div id="title">לומדת יסודות תהליך החניכה</div>
            <div class="start" @click="change">לתחילת הלומדה</div>
        </div>
        <div class="instructions" v-else>
            <div class="heading-container">
                <div class="heading">מטרת העל</div>
            </div>
            <div class="instruction-item">החניך יסביר את הגורמים המשפיעים על תהליך החניכה</div>
            <br><br>
            <div class="heading-container">
                <div class="heading">מטרות ביניים</div>
            </div>
            <div v-for="(goal, index) in goalsArray" :key="index" class="instruction-item">
                {{ goal }}
            </div>
            <button id="next" class="start" @click="nextPage">המשך</button>
        </div>
    </div>
</template>

<script>
export default {
  name: "start-screen",
  data() {
    return {
      showInstructions: false,
      goalsArray: [
        'החניך יגדיר מהי חניכה, עקרונותיה ומטרותיה',
        'החניך יפרט מהו משולש החניכה',
        'החניך יסביר מהו אירוע החניכה, סוגיו ועקרונותיו',
        'החניך יאפיין היבטים מרכזיים ומשפיעים של הנחנך',
        'החניך יגדיר סוגי חונכות ועקרונות בסיסיים בחונכות'
      ]
    }
  },
  methods: {
    change() {
      this.showInstructions = true;
    },
    nextPage() {
      this.$emit("switch-screen");
    },
  }
}
</script>

<style scoped>
#start-screen {
  font-family: "Heebo-bold";
  text-align: center;
  display: flex;
  justify-content: center;
}

.title {
  position: absolute;
  top: 30%;
  font-size: 9rem;
  color: #023E8A;
  font-weight: bold;
}

#title {
  animation: floatAnimation 3s ease-in-out infinite;
}

@keyframes floatAnimation {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
  100% {
    transform: translateY(0);
  }
}

.start {
  position: absolute;
  left: 50%;
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

.start:hover,
.start:focus {
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

.instructions {
  position: absolute;
  text-align: right;
  font-family: "Heebo";
  top: 50%;
  font-size: 1.6rem;
  transform: translateY(-50%);
  padding: 5rem;
  width: 50rem;
  border-radius: 10rem;
  background-color: #fff;
}

.instruction-item {
  padding: 0.5rem 1rem;
  border-radius: 10px;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
  display: inline-block; /* Allow the item to grow and shrink based on its content */
}

.instruction-item:hover {
  background-color: #e0f7fa; /* Light cyan background on hover */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.heading-container {
  position: relative;
  display: flex;
  text-align: right;
}

.heading {
  font-size: 2.6rem;
  color: #023E8A;
  margin-bottom: 1.2rem;
  font-family: "Heebo-bold";
  animation: floatAnimation 3s ease-in-out infinite;
  cursor: default;
  position: relative;
}

.heading::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  bottom: -5px; /* Position the line right below the text */
  left: 0;
  background-color: #023E8A;
  visibility: hidden;
  transform: scaleX(0);
  transition: all 0.3s ease-in-out 0s;
}

.heading:hover::before {
  visibility: visible;
  transform: scaleX(1);
}

#next {
  position: absolute;
  left: 23%;
  bottom: 5%;
}

</style>
