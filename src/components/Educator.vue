<template>
    <div id="educator">
      <navbar :titleIndex="4" @switch-page="switchPage"></navbar>
      <div class="title"> חונך </div>
    </div>
  </template>
  
  
  <script>
    import Navbar from '@/components/Navbar.vue';
 
  export default {
      name: 'educator',
      props: ['whereBeen'],
      data() {
          return {
          };
      },
      components: {
        Navbar
      },
      methods: {
        switchPage(index) {
        if (this.whereBeen.includes(index)) {
            this.$emit('switch-screen', index);
        }
      },
      },
  };
  </script>
  
  
  <style scoped>
  #educator {
  font-family: "Heebo";
  text-align: center;
  display: flex;
  justify-content: center;
  overflow-x: hidden;
  overflow-y: hidden;
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

  </style>
  