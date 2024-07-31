<template>
    <div id="job">
      <div class="back-home" @click="onSwitchPage"></div>
      <div>job</div>
    </div>
  </template>
  
  
  <script>


  export default {
      name: 'job',
      props: ['componentName'],
      data() {
          return {
              
          };
      },
      components: {
      },
      methods: {
        onSwitchPage() {
          this.$emit("add-green", this.componentName);
        }
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
  </style>
  