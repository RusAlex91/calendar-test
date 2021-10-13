<template>
  <div class="calendar">
    <div class="calendar__navigation">
      <h2 ref="date" class="calendar__month-year">Июнь 2021</h2>
      <div class="calendar-controls">
        <button
          @click="updateCalendar('descrease')"
          class="calendar-controls__left calendar-controls__inactive"
        >
          &#x3c;
        </button>
        <button
          @click="updateCalendar('increase')"
          class="calendar-controls__right"
        >
          &#x3e;
        </button>
      </div>
    </div>
    <hr />
    <div class="calendar__body" @click="populateCalendar">
      <div class="calendar-weekdays">
        <span>Понедельник</span>
        <span>Вторник</span>
        <span>Среда</span>
        <span>Четверг</span>
        <span>Пятница</span>
        <span>Суббота</span>
        <span>Воскресенье</span>
      </div>
      <div class="calendar-days">
        <calendar-day
          v-for="index in prevDates"
          :key="index"
          :index="index"
          :prev-date="true"
        ></calendar-day>
        <calendar-day
          v-for="(value, key, index) in day"
          :key="index"
          :dayInfo="value"
          :weekend="this.weekends"
        ></calendar-day>
        <calendar-day
          v-for="index in nextDates"
          :key="index"
          :index="index"
          :prev-date="true"
        ></calendar-day>
      </div>
    </div>
  </div>
</template>

<script>
import CalendarDay from './CalendarDay.vue'
export default {
  components: {
    CalendarDay
  },
  props: {
    holidaysData: {
      type: Array,
      required: false,
      default: () => [
        '16.10.2021',
        '5.10.2021',
        '1.1.2021',
        '2.1.2021',
        '3.1.2021',
        '4.1.2021',
        '5.1.2021',
        '6.1.2021',
        '7.1.2021',
        '8.1.2021',
        '23.2.2021',
        '8.3.2021',
        '1.5.2021',
        '9.5.2021',
        '12.6.2021',
        '4.11.2021'
      ]
    },
    tripsData: {
      type: Object,
      required: false,
      default: Object
    }
  },
  data () {
    return {
      date: new Date(),
      daysInMonth: null,
      prevDates: [],
      nextDates: [],
      currentDay: null,
      weekends: [],
      holidays: [],
      trips: [],
      tripData: {},
      holidayData: [],
      tripArr: [],
      day: {}
    }
  },
  methods: {
    updateCalendar (value) {
      if (value === 'descrease') {
        this.date.setMonth(this.date.getMonth() - 1)
        this.daysInMonth = null
        this.prevDates = []
        this.nextDates = []
        this.currentDay = null
        this.weekends = []
        this.trips = []
        this.tripArr = []
        this.day = {}
      } else if (value === 'increase') {
        this.date.setMonth(this.date.getMonth() + 1)
        this.daysInMonth = null
        this.prevDates = []
        this.nextDates = []
        this.currentDay = null
        this.weekends = []
        this.trips = []
        this.tripArr = []
        this.day = {}
      }
      this.createCalendar()
    },
    createCalendar () {
      const date = this.date

      date.setDate(1)

      this.daysInMonth = new Date(
        date.getFullYear(),
        date.getMonth() + 1,
        0
      ).getDate()

      const prevLastDay = new Date(
        date.getFullYear(),
        date.getMonth(),
        0
      ).getDate()

      const lastDayIndex = new Date(
        date.getFullYear(),
        date.getMonth() + 1,
        0
      ).getDay()

      const months = [
        'Январь',
        'Февраль',
        'Март',
        'Апрель',
        'Май',
        'Июнь',
        'Июль',
        'Август',
        'Сентябрь',
        'Октябрь',
        'Ноябрь',
        'Декабрь'
      ]
      // month and year
      this.$refs.date.innerText = `${
        months[date.getMonth()]
      } ${date.getFullYear()}`

      this.prevDates = []
      const firstDayIndex = date.getDay() - 1

      for (let x = firstDayIndex; x > 0; x--) {
        const temp = prevLastDay - x + 1
        this.prevDates.push(temp)
      }

      this.nextDates = []
      const nextDays = 7 - lastDayIndex

      for (let o = 1; o <= nextDays; o++) {
        const temp = o
        this.nextDates.push(temp)
      }

      // Сегоднящний день, для отображения на календаре (не доделано)
      this.currentDay = new Date().getDate()

      const month = this.date.getMonth() + 1
      var current = new Date(this.date.getFullYear(), month - 1, 1)
      const objDay = {}

      const daysArr = [...Array(this.daysInMonth).keys()]

      for (let currentDay = 0; currentDay < daysArr.length; currentDay++) {
        let today = this.date
        const dd = daysArr[currentDay]
        const mm = month
        const yyyy = today.getFullYear()

        today = dd + '.' + mm + '.' + yyyy

        objDay[currentDay] = {}
        objDay[currentDay].day = currentDay + 1
        objDay[currentDay].weekend = false

        this.holidayData.forEach(el => {
          if (today === el) {
            this.holidays.push(dd)

            objDay[dd - 1].holidays = true
          }
        })

        Object.entries(this.tripData).forEach(([key, value]) => {
          value.forEach(el => {
            if (today === el) {
              this.trips.push(dd)
              objDay[dd - 1].trip = true
              objDay[dd - 1].location = key
            }
          })
        })
      }
      let dd = 0
      while (current.getMonth() === month - 1) {
        if (current.getDay() === 0 || current.getDay() === 6) {
          this.weekends.push(current.getDate())
          objDay[dd].weekend = true
        }

        // move to next day
        current.setDate(current.getDate() + 1)
        dd++
      }
      this.day = objDay
    }
  },

  mounted () {
    this.createCalendar()
  },
  updated () {
    this.holidayData = this.holidaysData
  },
  watch: {
    tripsData: function () {
      this.tripData = this.tripsData
      this.createCalendar()
    }
  }
}
</script>

<style scoped lang="scss">
.calendar {
  /* .calendar__navigation */
  width: 90.6rem;
  height: 65.4rem;
  background-color: #fff;
  justify-content: center;
  align-items: center;
  padding: 2.7rem;
  margin-bottom: 7rem;
  border-radius: 1rem;
  &__navigation {
    display: flex;
  }

  /* .calendar__month-year */

  &__month-year {
    font-size: 3.2rem;
    line-height: 4.8rem;
    font-weight: 700;
  }

  /* .calendar__body */

  &__body {
    margin-bottom: 6.6rem;
  }
}

.calendar-controls {
  /* .calendar-controls__left */
  margin-left: auto;

  &__left {
    cursor: pointer;
    width: 3.5rem;
    height: 3.5rem;
    border-radius: 2rem;
    background-color: #0078d2;
    font-size: 2rem;
    color: white;
  }

  /* .calendar-controls__right */

  &__right {
    cursor: pointer;
    margin: 5px;
    width: 3.5rem;
    height: 3.5rem;
    border-radius: 2rem;
    background-color: #0078d2;
    font-size: 2rem;
    color: white;
  }

  &__inactive {
    background-color: #00426912;
    color: #00395ccc;
  }
}

.calendar-weekdays {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  margin-top: 35px;
  font-weight: 700;
  font-size: 12px;
  line-height: 1.4rem;
  margin-bottom: 1rem;
}
.calendar-days {
  /* .calendar-days__prev-date */
  display: grid;
  grid-template-columns: repeat(7, 0fr);
  border: 1px solid #e9e9e9;
  // well, this is bad... sorry for that, i just cant make it right
  height: 47rem;
  overflow: hidden;

  /* .calendar-days__next-date */

  div {
    width: 12.74rem;
    height: 9.2rem;
    border: 1px solid #e9e9e9;
  }
}

hr {
  border: 1px solid #00416633;
  opacity: 0.2;
}
</style>
