<template>
  <div class="employees-list">
    <h3 class="employees-list__title">Сотрудник</h3>
    <select name="" id="em-list">
      <option value="Алексей Лечащий">Алексей Лечащий</option>
      <option value="Алексей Лечащий 2">Алексей Лечащий 2</option>
      <option value="Алексей Лечащий 3">Алексей Лечащий 3</option>
    </select>
  </div>
</template>

<script>
export default {}
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

#em-list {
  margin: auto;
  height: 4rem;
  width: 38rem;
}
</style>
