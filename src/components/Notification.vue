<template>
  <div>{{ notification }}</div>
</template>

<script>
export default {
  name: 'Notification',
  props: ['notification'],
};
</script>

<style lang="scss" scoped>
div:empty {
  display: none;
}
div {
  display: inline-block;
  border-radius: 50px;
  color: #fff;
  font-size: 0.8em;
  letter-spacing: 0.35em;
  background-color: #31323D;
  padding: .8rem;
  margin: auto;
}
</style>
