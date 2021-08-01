<template>
  <div id="container">
    <h1>Color Pallete Generator</h1>
    <ColorPallete :colors="colors" />
    <RegenerateButton @regenerate="regenerate" />
  </div>
</template>

<script>
import axios from 'axios';
import ColorPallete from '@/components/ColorPallete.vue';
import RegenerateButton from '@/components/RegenerateButton.vue';

export default {
  name: 'App',
  components: {
    ColorPallete,
    RegenerateButton,
  },
  data() {
    return {
      fetched: false,
      colors: [],
    };
  },
  methods: {
    async getColorPallete() {
      try {
        const url = 'http://colormind.io/api/';
        const data = {
          model: 'default',
          headers: {
            'Content-Type': 'application/json',
          },
        };
        const response = await axios.post(url, JSON.stringify(data));
        this.toHex(response.data.result);
      } catch (error) {
        console.error(error);
      }
    },
    toHex(listOfData) {
      const listOfHex = listOfData.flat().map((x) => x.toString(16));
      for (let i = 0; i < listOfHex.length; i += 3) {
        this.colors.push(`#${listOfHex.slice(i, i + 3).join('')}`);
      }
    },
    regenerate() {
      this.colors = [];
      this.getColorPallete();
    },
  },
  mounted() {
    if (!this.fetched) {
      this.fetched = true;
      this.getColorPallete();
    }
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html, body, #app, #container {
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

body {
  color: #31323D;
  background-color: #F0F0F0;
}

h1 {
  margin: 2rem 0;
}
</style>
