<template>
  <div id="container">
    <Notification :notification="notification" />
    <h1>Color Pallete Generator</h1>
    <ColorPallete :colors="colors" @copyToClipboard="copyToClipboard" />
    <RegenerateButton @regenerate="regenerate" />
    <p>Or just press the "Spacebar" to generate new palettes.</p>
  </div>
</template>

<script>
import axios from 'axios';
import ColorPallete from '@/components/ColorPallete.vue';
import RegenerateButton from '@/components/RegenerateButton.vue';
import Notification from '@/components/Notification.vue';

export default {
  name: 'App',
  components: {
    ColorPallete,
    RegenerateButton,
    Notification,
  },
  data() {
    return {
      fetched: false,
      colors: [],
      notification: '',
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
    copyToClipboard(color) {
      navigator.clipboard.writeText(color);
      this.notification = `Color ${color} copied to your clipboard`;
    },
  },
  mounted() {
    window.addEventListener('keyup', (event) => {
      if (event.key === ' ') {
        this.regenerate();
      }
    });
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

#app {
  display: flex;
  align-items: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

body {
  color: #31323D;
  background-color: #F0F0F0;
}

#container {
  flex-grow: 1;
  padding: 1rem 0;
}

h1, p {
  margin: 2rem 0;
}

@media screen and (min-width: 768px) {
  html, body, #app {
    height: 100%;
  }
}
</style>
