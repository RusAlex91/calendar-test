<template>
  <div class="employees-list">
    <h3 class="employees-list__title">Сотрудник</h3>
    <employee-select @input="change" :options="this.option"> </employee-select>
    {{ datadata }}
  </div>
</template>

<script>
import EmployeeSelect from './EmployeeSelect.vue'
export default {
  components: {
    EmployeeSelect
  },
  data () {
    return {
      datadata: null,
      option: {
        1: {
          option: 'Лозх',
          images: 'https://via.placeholder.com/32x32/f00'
        },
        2: {
          option: 'Дыа',
          images: 'https://via.placeholder.com/32x32/#990'
        }
      }
    }
  },
  methods: {
    change (data) {
      this.datadata = data
    }
  }
}
</script>

<style lang="scss">
.employees-list {
  width: 43.8rem;
  height: 14.3rem;
  background-color: #fff;
  border-radius: 20px;

  &__title {
    font-size: 2.2rem;
    line-height: 2.2rem;
    margin-top: 30px;
    margin-left: 40px;
    margin-bottom: 20px;
  }
}

.custom-select {
  margin-left: 40px;
}
</style>
