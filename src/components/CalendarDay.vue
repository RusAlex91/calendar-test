<template>
  <div class="day" :class="{ today: currentDay }">
    <span class="day_number">{{ index }}</span>

    <!-- <span v-if="trip" class="day__trip-name">Екатеринбург</span>
    <span v-if="weekend">Выходной</span>
    <span v-if="selebration">Праздник</span> -->
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
    }
  },
  data () {
    return {
      currentDay: null
    }
  },
  methods: {
    isWeekend () {}
  },
  mounted () {
    if (this.day === this.index) {
      this.currentDay = true
    } else {
      this.currentDay = false
    }
    this.isWeekend()
    console.log(this.index)
  }
}
</script>

<style scoped lang="scss">
.day {
  /* .day_number */
  width: 9rem;
  height: 12rem;
  border: 1px solid turquoise;
  &_number {
  }

  /* .day__trip-name */

  &__trip-name {
  }
}
.today {
  background: rgba(255, 99, 71, 0.295);
}
</style>
