<template>
  <div class="hour">
    <div class="item" v-for="item in items" :key="item.id"></div>
  </div>
</template>

<script>
export default {
  props: {
    items: Array
  },
  data() {
    return {};
  }
};
</script>

<style lang="scss" scoped>
.item {
  height: 48px;

  &::after {
    border-top: #dadce0 1px solid;
    content: "";
    position: absolute;
    width: 100%;
  }
}
</style>
