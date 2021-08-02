<template>
  <div>
    <button @click="$emit('regenerate')">Generate Pallete</button>
  </div>
</template>

<script>
export default {
  name: 'RegenerateButton',
};
</script>

<style lang="scss" scoped>
button {
  cursor: pointer;
  box-shadow: inset 0 0 1em rgba(251,81,81,0.4), 0 0 1em rgba(251,81,81,0.4);
  border: #fb5454 solid 2px;
  border-radius: 0;
  color: #fb5454;
  background: none;
  font-size: 0.8em;
  letter-spacing: 0.35em;
  transition: background-color 0.3s, box-shadow 0.3s, color 0.3s;
  padding: 1.2em 5em;
  &:hover, &:active {
    box-shadow: inset 0 0 0 rgba(251,81,81,0.4), 0 0 1.5em rgba(251,81,81,0.6);
    color: rgba(255,255,255,1);
    background-color: #fb5454;
  }
}
</style>
