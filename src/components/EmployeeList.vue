<template>
  <div class="employees-list">
    <h3 class="employees-list__title">Сотрудник</h3>
    <employee-select> </employee-select>
  </div>
</template>

<script>
import EmployeeSelect from './EmployeeSelect.vue'
export default {
  components: {
    EmployeeSelect
  }
}
</script>

<style scoped lang="scss">
.employees-list {
  width: 43.8rem;
  height: 14.3rem;
  background-color: #fff;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  &__title {
    font-size: 2.2rem;
    line-height: 2.2rem;
    margin: 3rem 3rem 1rem;
  }
}
</style>
