/* eslint-disable indent */
<template>
  <div class="custom-select" :tabindex="tabindex" @blur="open = false">
    <div class="selected" :class="{ open: open }" @click="open = !open">
      <img class="select-img" :src="this.image" />
      {{ selected }}
    </div>
    <div class="items" :class="{ selectHide: !open }">
      <div
        v-for="(option, i) in options"
        :key="i"
        @click="
          ;(selected = option.option),
            (open = false),
            $emit('input', option.option),
            (image = option.images)
        "
      >
        <img class="select-img" :src="option.images" alt="" />
        {{ option.option }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Object,
      required: true
    },
    default: {
      type: String,
      required: false,
      default: 'Выберите сотрудника'
    },
    tabindex: {
      type: Number,
      required: false,
      default: 0
    }
  },
  data () {
    return {
      image: null,
      selected: this.default
        ? this.default
        : this.options.length > 0 // eslint-disable-next-line indent
        ? this.options[0] // eslint-disable-next-line indent
        : null,
      open: false
    }
  },
  mounted () {
    this.$emit('input', this.selected)
  }
}
</script>

<style scoped>
.custom-select {
  position: relative;
  width: 330px;
  text-align: left;
  outline: none;
  height: 40px;
  line-height: 42px;
}

.custom-select .selected {
  display: flex;
  align-items: center;
  background-color: transparent;
  border-radius: 6px;
  border: 1px solid #00426947;
  color: #000;
  padding-left: 1em;
  cursor: pointer;
  user-select: none;
  border-radius: 5px;
  line-height: 42px;
  font-weight: 400;
  font-size: 1.6rem;
}

.custom-select .selected img {
  margin-right: 1rem;
}

.custom-select .selected.open {
  border: 1px solid lightblue;
  border-radius: 6px 6px 0px 0px;
}

.custom-select .selected:after {
  position: absolute;
  content: '';
  top: 22px;
  right: 2rem;
  width: 0;
  height: 0;
  border: 4px solid transparent;
  border-color: #00203359 transparent transparent transparent;
}

.custom-select .selected:before {
  position: absolute;
  content: '';
  border-left: 1px solid #00426947;
  width: 50px;
  height: 43px;

  top: 1px;
  left: 280px;
}

.custom-select .items {
  font-size: 1.6rem;
  color: #000;
  border-radius: 0px 0px 6px 6px;
  overflow: hidden;
  border-right: 1px solid lightblue;
  border-left: 1px solid lightblue;
  border-bottom: 1px solid lightblue;
  position: absolute;
  background-color: #fff;
  left: 0;
  right: 0;
  z-index: 1;
}

.custom-select .items div {
  display: flex;
  align-items: center;
  color: #000;
  padding-left: 1em;
  cursor: pointer;
  user-select: none;
}

.custom-select .items div img {
  margin-right: 1rem;
}

.custom-select .items div img {
}

.custom-select .items div:hover {
  background-color: #0078d2;
}

.selectHide {
  display: none;
}

.select-img {
  border-radius: 20px;
}
</style>
