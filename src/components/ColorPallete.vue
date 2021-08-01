<template>
  <div id="color-pallete">
    <div
      class="colors"
      v-for="color in colors"
      :key="color"
    >
      <div>
        <div
          class="color"
          :style="{ 'background-color': color }"
        >
        </div>
        <p>{{ color }}</p>
      </div>
    </div> </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'ColorPallete',
  data() {
    return {
      colors: [],
    };
  },
  methods: {
    toHex(listOfData) {
      const listOfHex = listOfData.flat().map((x) => x.toString(16));
      for (let i = 0; i < listOfHex.length; i += 3) {
        this.colors.push(`#${listOfHex.slice(i, i + 3).join('')}`);
      }
    },
  },
  mounted() {
    (async () => {
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
    })();
  },
};
</script>

<style lang="scss" scoped>
#color-pallete {
  display: flex;
  justify-content: center;
  align-items: center;
  .colors {
    cursor: pointer;
    border-radius: 10px;
    width: 100%;
    max-width: 150px;
    flex-grow: 1;
    padding: 10px 10px 0 10px;;
    margin: 0 10px;
    background-color: #fff;
    .color {
      height: 200px;
    }
    p {
      margin: 10px;
    }
  }
}

@media screen and (max-width: 768px) {
  #color-pallete {
    flex-direction: column;
    .colors {
      max-width: 400px;
      flex-grow: 0;
      margin: 10px 0;
      .color {
        height: 70px;
      }
    }
  }
}
</style>
