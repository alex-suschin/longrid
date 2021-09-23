<template>
  <div id="app">
    <h1>Плиточки</h1>
    <Article />
  </div>
</template>

<script>
import Article from '@/components/Article.vue';

export default {
  components: { Article },
  name: "App"
};
</script>

<style lang="scss">
#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
.loader {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: rgba(0,0,0,.8);
  font-size: 172px;
  z-index: 99;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 700;
}

</style>
