<template>
  <ColorPallete msg="Welcome to Your Vue.js App"/>
</template>

<script>
import ColorPallete from '@/components/ColorPallete.vue';

export default {
  name: 'App',
  components: {
    ColorPallete,
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html, body, #app, #color-pallete {
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

body {
  background-color: #F0F0F0;
}
</style>
