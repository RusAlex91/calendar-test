<template>
  <div class="planning">
    <nav>
      <navigation></navigation>
    </nav>
    <main>
      <div class="claendar-wrapper">
        <h1>Планирование</h1>
        <calendar :tripsData="trips" :holidaysData="holidaysData"></calendar>
      </div>
      <div class="employee">
        <employee-list
          @trips="getTripData"
          :employeeData="employeeData"
        ></employee-list>
        <employee-details
          :tripsDays="tripsDays"
          :tripsCounter="tripsCounter"
        ></employee-details>
      </div>
    </main>
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue'
import Calendar from './components/Calendar.vue'
import EmployeeList from './components/EmployeeList.vue'
import EmployeeDetails from './components/EmployeeDetails.vue'

export default {
  name: 'App',
  components: {
    Navigation,
    Calendar,
    EmployeeList,
    EmployeeDetails
  },
  data () {
    return {
      employeeData: null,
      holidaysData: null,
      trips: null,
      tripsDays: null,
      tripsCounter: null
    }
  },
  methods: {
    getTripData (data) {
      this.trips = data

      this.tripsCounter = Object.keys(this.trips).length
      this.tripsDays = null
      Object.entries(this.trips).forEach(([key, value]) => {
        this.tripsDays += value.length
      })
    }
  },
  created () {
    fetch(
      'https://my-json-server.typicode.com/RusAlex91/calendar-test/holidays',
      {}
    )
      .then(response => response.json())
      .then(data => (this.holidaysData = data))
  },
  mounted () {
    fetch(
      'https://my-json-server.typicode.com/RusAlex91/calendar-test/employees',
      {}
    )
      .then(response => response.json())
      .then(data => (this.employeeData = data))
  },
  updated () {}
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed:ital,wght@0,300;0,400;0,700;1,300;1,400;1,700&display=swap');
#app {
  font-family: 'Roboto Condensed', sans-serif;
  background: #e5e5e5;
}

//temporary reset
* {
  margin: 0;
  padding: 0;
}

button {
  border: none;
  margin: 0;
  padding: 0;
  width: auto;
  overflow: visible;

  background: transparent;

  /* inherit font & color from ancestor */
  color: inherit;
  font: inherit;

  /* Normalize `line-height`. Cannot be changed from `normal` in Firefox 4+. */
  line-height: normal;
}

//1 rem = 10px
html {
  font-size: 62.5%;
}

#app {
  display: flex;
  justify-content: center;
}

.planning {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

nav {
  margin-top: 4rem;
}

main {
  display: flex;
}

.claendar-wrapper {
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
  row-gap: 3rem;
}

h1 {
  font-size: 7.2rem;
  line-height: 8.64rem;
  font-weight: 700;
}

.employee {
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  margin: 3rem;
}
</style>
