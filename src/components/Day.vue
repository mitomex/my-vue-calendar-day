<template>
  <div class="day">
    <div class="header">
      <p>
        <span>Current time:</span>
        <span>{{ currentTime.hour }}:</span>
        <span>{{ currentTime.minute }}:</span>
        <span>{{ currentTime.second }}</span>
      </p>
    </div>
    <div class="main">
      <div class="presentation">
        <div class="presentation-inner">
          <div class="label">
            <TimeLabel :items="items" />
          </div>
          <div class="data">
            <Hour :items="items" />
            <div class="vertical"></div>
            <div class="current" :style="{ top: positionY + 'px' }"></div>
          </div>
        </div>
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

const toDoubleDigit = item => {
  return item < 10 ? "0" + item : item;
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
  computed: {
    currentMinutes() {
      return (
        parseInt(this.currentTime.hour) * 60 + parseInt(this.currentTime.minute)
      );
    },
    positionY() {
      return (this.currentMinutes * 1152) / (24 * 60);
    }
  },
  methods: {
    updateTime(date) {
      this.currentTime.hour = toDoubleDigit(date.getHours());
      this.currentTime.minute = toDoubleDigit(date.getMinutes());
      this.currentTime.second = toDoubleDigit(date.getSeconds());

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
  overflow: hidden;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
.main {
  position: absolute;
  top: 63px;
  right: 0;
  bottom: 0;
  left: 0;
}
.presentation {
  overflow-x: auto;
  overflow-y: scroll;
  position: relative;
  height: 100%;

  /* always display a scrollbar. */
  &::-webkit-scrollbar {
    width: 16px;
    height: 16px;
  }
  &::-webkit-scrollbar-thumb {
    background: #dadce0;
    border: 4px solid #fff;
    border-radius: 8px;
  }
}
.presentation-inner {
  display: flex;
  flex: 1 1 auto;
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
.current {
  background-color: red;
  position: absolute;
  left: 0;
  width: 100%;
  height: 1px;
}
</style>
