<template>
  <div class="employee-details">
    <div class="employee-details__trips">
      <span class="employee-details__trips-number">{{ tripCounter }}</span>
      <span class="employee-details__text">поездки</span>
    </div>

    <div class="employee-details__days">
      <span class="employee-details__days-in-trips">{{ tripDays }}</span>
      <span class="employee-details__text">дней командировки</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tripsCounter: {
      type: Number,
      required: false,
      default: 0
    },
    tripsDays: {
      type: Number,
      required: false,
      default: 0
    }
  },
  data () {
    return {
      tripCounter: 0,
      tripDays: 0
    }
  },

  updated () {
    this.tripCounter = this.tripsCounter
    this.tripDays = this.tripsDays
  }
}
</script>

<style scoped lang="scss">
.employee-details {
  /* .employee-details__trips */
  width: 43.8rem;
  height: 16.6rem;
  background-color: #fff;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  row-gap: 2rem;
  &__trips {
    display: flex;
    margin-left: 4rem;
    margin-right: 4rem;
    align-items: center;
    border-bottom: 1px solid rgba(0, 65, 102, 0.2);
    min-height: 40%;
  }

  /* .employee-details__trips-number */

  &__trips-number {
    font-weight: 400;
    font-size: 3.2rem;
    line-height: 3.9rem;
  }

  /* .employee-details__days */

  &__days {
    display: flex;
    margin-left: 4rem;
    margin-right: 4rem;
    align-items: center;
  }

  /* .employee-details__days-in-trips */

  &__days-in-trips {
    font-weight: 400;
    font-size: 3.2rem;
    line-height: 3.9rem;
  }
  &__text {
    margin-left: auto;
    font-weight: 400;
    font-size: 1.6rem;
    line-height: 17px;
  }
}
</style>
