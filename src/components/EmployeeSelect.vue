<template>
  <el-select v-model="value" value-key="value" placeholder="Select">
    <template><img class="prefix" :src="value.photo"/></template>
    <el-option
      v-for="item in outlet"
      :key="item.value"
      :label="item.label"
      :value="item"
    >
      <img :src="item.photo" /> {{ item.label }}
    </el-option>
  </el-select>
</template>

<script>
export default {
  data () {
    return {
      outlet: [
        {
          value: 'mcd',
          label: 'McDonald',
          photo:
            'https://upload.wikimedia.org/wikipedia/commons/5/50/McDonald%27s_SVG_logo.svg'
        },
        {
          value: 'kfc',
          label: 'KFC',
          photo:
            'http://www.kfcku.com/themes/kfc_indonesia/images/kfc-indonesia-logo.png'
        },
        {
          value: 'pizzahut',
          label: 'Pizza Hut',
          photo:
            'https://vignette.wikia.nocookie.net/logopedia/images/b/b3/Pizza_Hut_Logo_2.png/revision/latest?cb=20161129133747'
        }
      ],
      value: null
    }
  },
  created () {
    this.value = this.outlet[0]
  }
}
</script>

<style>
img {
  width: 20px;
  height: 20px;
}
</style>
