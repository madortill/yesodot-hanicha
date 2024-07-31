<template>
  <div id="navbar">
    <div class="container">
      <nav>
        <ul>
          <li
            v-for="(hebrewTitle, name) in titles"
            :key="name"
            :class="{ active: componentName === name, disabled: !whereBeen.includes(name) }"
            @click="chosenTitle(name)"
          >
            {{ hebrewTitle }}
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
    name: 'navbar',
    props: ["componentName", "whereBeen"],
    data() {
        return {
            titles: {
                "introduction": "מבוא",
                "triangle": "משולש החניכה",
                "event": "אירוע החניכה",
                "educated": "נחנך",
                "educator": "חונך",
                "summery": "סיכום",
            }

        };
    },
    methods: {
        chosenTitle(name) {
          if (this.whereBeen.includes(name))
            this.$emit('go-to-page', name);
        },
    },
};
</script>
<style scoped>
.container {
  height: 10vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
  align-content: flex-start;
  flex-wrap: wrap;
  margin-top: 2%;
}

@media (max-width: 1024px) {
  .container {
    height: 10vh;
    width: 75vw;
    margin-top: 2%;
    position: relative;
    left: 30%;
    transform: translateX(-50%);
  }
}

* {
  margin: 0;
  box-sizing: border-box;
}

nav {
  background: #fff;
  border-radius: 50px;
  box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
}

nav ul li {
  padding: 0;
  list-style: none;
  display: inline-block;
  padding: 0.5vw 2vw;
  margin: 1vw;
  font-size: 1.2rem;
  font-weight: 500;
  color: #777;
  position: relative;
  z-index: 2;
  cursor: pointer;
  transition: color 0.5s;
}

nav ul li.active {
  background: #023e8a;
  border-radius: 30px;
  color: white;
}

.disabled {
  cursor: default;
}
</style>
