<template>
  <div class="time-label">
    <div class="item" v-for="item in items" :key="item.id">
      <span class="time">{{ item.label }}</span>
    </div>
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
  text-align: right;
}
.time {
  color: #70757a;
  display: block;
  font-size: 10px;
  position: relative;
  top: -6px;
}
</style>
