<template>
  <div class="skeleton">
    <div class="skeleton-line" v-for="n in lines" :key="n"></div>
  </div>
</template>

<script>
export default {
  props: {
    lines: {
      type: Number,
      default: 5,
    },
  },
};
</script>

<style scoped>
.skeleton {
  background-color: #f2f2f2;
  border-radius: 5px;
  margin: 30px 0;
  padding: 20px;
  width: 50vw;
  height: 40vw;
}

.skeleton-line {
  background-color: #ddd;
  height: 100px;
  margin: 10px 0;
  width: 100%;
}
</style>
