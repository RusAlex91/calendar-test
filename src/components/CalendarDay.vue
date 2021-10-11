<template>
  <div class="day" :class="{ today: currentDay, weekend: todayWeekend }">
    <span class="day_number">{{ index }}</span>
    <span
      v-if="trip && !todayWeekend"
      :class="{ tripBadge: trip }"
      class="day__trip-name"
      >Екатеринбург</span
    >
    <span v-if="todayWeekend" :class="{ weekendBadge: todayWeekend }"
      >Выходной</span
    >
    <span v-if="holidays">Праздник</span>
  </div>
</template>

<script>
export default {
  props: {
    index: {
      type: Number,
      required: true,
      default: null
    },
    day: {
      type: Number,
      required: false,
      default: null
    },
    weekend: {
      type: Array,
      required: false,
      default: Array
    },
    trip: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      currentDay: null,
      weekends: this.weekend,
      todayWeekend: false
    }
  },
  methods: {
    isWeekend () {
      this.weekends.forEach(el => {
        if (el === this.index) {
          this.todayWeekend = true
        }
      })
    }
  },
  mounted () {
    if (this.day === this.index) {
      this.currentDay = true
    } else {
      this.currentDay = false
    }
    this.weekends = this.weekend
    this.isWeekend()
  },
  created () {}
}
</script>

<style scoped lang="scss">
.day {
  /* .day_number */
  display: flex;
  flex-direction: column;
  align-items: flex-end;

  width: 9rem;
  height: 12rem;
  border: 1px solid turquoise;
  &_number {
    font-size: 1.6rem;
    margin: 7px;
  }

  /* .day__trip-name */

  &__trip-name {
  }
}
.today {
  background: rgba(255, 99, 71, 0.295);
}

.weekend {
  background: #fcfcfc;
}

.weekendBadge {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: auto;
  margin-bottom: 1rem;
  margin-right: 1rem;
  font-size: 14px;
  font-weight: 400;
  width: 7.2rem;
  height: 2.3rem;
  background: #97b2c4;
  border-radius: 5px;
}

.tripBadge {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: auto;
  margin-bottom: 1rem;
  margin-right: 1rem;
  font-size: 12px;
  font-weight: 400;
  line-height: 2rem;
  padding-left: 1rem;
  padding-right: 1rem;
  background: #97b2c4;
  border-radius: 5px;
}
</style>
