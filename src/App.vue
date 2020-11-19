<template>
  <div id="app">
    <img alt="Now Loading Icon" src="./assets/icon.png">
    <icon-layer>
      <clock-view/>
    </icon-layer>
  </div>
</template>

<script>
import IconLayer from 'vue-feather-icon-set';
import ClockView from './components/ClockView.vue';

export default {
  name: 'App',
  components: {
    ClockView,
    IconLayer,
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html, body {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fbfeff;
  background-color: #313131;

  img {
    width: 10vw;
  }
}
</style>
