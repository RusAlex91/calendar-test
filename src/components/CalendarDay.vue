<template>
  <div
    class="day"
    :class="{ today: currentDay, weekend: dayInfo.weekend }"
    @click="this.getColors"
  >
    <span class="day__number" v-if="prevDate && !nextDate">{{ index }}</span>
    <span class="day__number" v-if="nextDate && !prevDate">{{ index }}</span>
    <span class="day__number">{{ dayInfo.day }}</span>
    <span
      v-if="dayInfo.trip && !dayInfo.weekend"
      :class="{ tripBadge: dayInfo.trip }"
      class="day__trip-name"
      >{{ dayInfo.location }}</span
    >
    <span
      v-if="dayInfo.weekend && !dayInfo.holidays"
      :class="{ weekendBadge: dayInfo.weekend }"
      >Выходной</span
    >
    <span v-if="dayInfo.holidays" :class="{ holidayBadge: dayInfo.holidays }"
      >Праздник</span
    >
  </div>
</template>

<script>
export default {
  props: {
    index: {
      type: Number,
      required: false,
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
    holiday: {
      type: Array,
      required: false,
      default: Array
    },
    trip: {
      type: Array,
      default: Array
    },
    dayInfo: {
      type: Object,
      default () {
        return {
          day: null,
          weekend: false,
          trip: false,
          location: ''
        }
      }
    },
    prevDate: {
      type: Boolean,
      default: false
    },
    nextDate: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      currentDay: null,
      weekends: this.weekend,

      locationColors: null
    }
  },
  methods: {
    getColors () {
      fetch(
        'https://my-json-server.typicode.com/RusAlex91/calendar-test/locationColors'
      )
        .then(response => response.json())
        .then(data =>
          Object.entries(data).forEach(([key, value]) => {
            debugger
            if (this.dayInfo.location === key) {
              console.log(value)
            }
          })
        )
    }
  },
  created () {},
  mounted () {
    if (this.day === this.index) {
      this.currentDay = true
    } else {
      this.currentDay = false
    }
    console.log('mounted')
  },
  beforeUpdate () {
    this.currentDay = false
  },
  updated () {}
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
  &__number {
    font-size: 1.6rem;
    margin: 7px;
  }

  /* .day__trip-name */
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

.holidayBadge {
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
</style>
