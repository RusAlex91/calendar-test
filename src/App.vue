<template>
  <nav>
    <navigation></navigation>
  </nav>
  <main>
    <div class="claendar-wrapper">
      <h1>Планирование</h1>
      <calendar></calendar>
    </div>
    <div class="employee">
      <employee-list></employee-list>
      <employee-details></employee-details>
    </div>
  </main>
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
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
