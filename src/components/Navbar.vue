<template>
    <div id="navbar">
        <div class="container">
            <nav>
                <ul @click="chosenTitle">
                    <li :class="{ active: titleIndex === 0 }">מבוא</li>
                    <li :class="{ active: titleIndex === 1 }">משולש החניכה</li>
                    <li :class="{ active: titleIndex === 2 }">אירוע החניכה</li>
                    <li :class="{ active: titleIndex === 3 }">נחנך</li>
                    <li :class="{ active: titleIndex === 4 }">חונך</li>
                    <li :class="{ active: titleIndex === 5 }">סיכום</li>
                </ul>
            </nav>
        </div>
    </div>
</template>
  
<script>
export default {
    name: 'navbar',
    props: ["titleIndex"],
    data() {
        return {

        };
    },
    methods: {
        chosenTitle(event) {
            if (event.target.tagName === "li") {
                this.titleIndex = parseInt(event.target.id.slice(-1)) - 1;
                this.$emit('chosen-page', this.titleIndex);
            }
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
    cursor: default;
    transition: color 0.5s;
}

nav ul li.active {
    background: #023E8A;
    cursor: pointer;
    border-radius: 30px;
    color: white;
}
</style>
  