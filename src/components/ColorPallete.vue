<template>
  <div id="color-pallete">
    <div
      class="colors"
      v-for="color in colors"
      :key="color"
      @click="$emit('copyToClipboard', color)"
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
export default {
  name: 'ColorPallete',
  props: ['colors'],
};
</script>

<style lang="scss" scoped>
#color-pallete {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 2rem 0;
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
