<template>
  <ul class="navigation">
    <li><a href="">Главная</a></li>
    <li><a href="">Сервисы</a></li>
    <li class="selected"><a href="">Планирование</a></li>
  </ul>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.navigation {
  display: flex;
  column-gap: 4.8rem;
  font-weight: 400;
  font-size: 1.8rem;
  line-height: 2.7rem;
}

.navigation li {
  list-style: none;
  position: relative;
  display: inline-block;
}

.navigation li::after {
  content: '>';
  position: relative;
  left: 20px;
}

.navigation li:last-child::after {
  content: '';
}

.navigation li a {
  color: inherit;
  text-decoration: none;
}
</style>
