<template>
  <div id="educator">
    <div class="title">חונך</div>
  </div>
</template>

<script>
export default {
  name: "educator",
  data() {
    return {};
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
  font-family: "Heebo-bold";
  color: #0077b6;
  width: 100vw;
}
</style>
