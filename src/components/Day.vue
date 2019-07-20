<template>
  <div>
    <p>
      <span>Current time:</span>
      <span>{{ currentTime.hour }}:</span>
      <span>{{ currentTime.minute }}:</span>
      <span>{{ currentTime.second }}</span>
    </p>
    <div class="day">
      <div class="label">
        <TimeLabel :items="items" />
      </div>
      <div class="data">
        <Hour :items="items" />
        <div class="vertical"></div>
      </div>
    </div>
  </div>
</template>

<script>
import TimeLabel from "./TimeLabel";
import Hour from "./Hour";

const items = [];

const dayTimes = () => {
  for (let i = 0; i < 24; i++) {
    items.push({
      id: i + 1,
      label: i + ":00"
    });
  }
};

export default {
  data() {
    return {
      items: items,
      currentTime: {
        hour: "",
        minute: "",
        second: ""
      }
    };
  },
  components: {
    TimeLabel,
    Hour
  },
  computed: {},
  methods: {
    updateTime(date) {
      this.currentTime.hour =
        date.getHours() < 10 ? "0" + date.getHours() : date.getHours();
      this.currentTime.minute =
        date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes();
      this.currentTime.second =
        date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();

      setTimeout(() => {
        this.updateTime(new Date());
      }, 1000 - new Date().getMilliseconds());
    }
  },
  mounted() {
    dayTimes();
    this.updateTime(new Date());
  }
};
</script>

<style lang="scss" scoped>
.day {
  display: flex;
}
.label {
  display: inline-flex;
  min-width: 40px;
  position: relative;
}
.data {
  display: inline-flex;
  position: relative;
  width: 100%;
}
.vertical {
  border-right: 1px solid #dadce0;
  width: 8px;
}
</style>
