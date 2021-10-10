<template>
  <div class="calendar">
    <div class="calendar__navigation">
      <h2 class="calendar__month-year">Июнь 2021</h2>
      <div class="calendar-controls">
        <button class="calendar-controls__left calendar-controls__inactive">
          &#x3c;
        </button>
        <button class="calendar-controls__right">&#x3e;</button>
      </div>
    </div>
    <hr />
    <div class="calendar__body">
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
        <div class="prev-date__date">31</div>

        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
        <div>9</div>
        <div>10</div>
        <div>11</div>
        <div>12</div>
        <div>13</div>
        <div>14</div>
        <div>15</div>
        <div>16</div>
        <div>17</div>
        <div>18</div>
        <div>19</div>
        <div>20</div>
        <div>21</div>
        <div>22</div>
        <div>23</div>
        <div>24</div>
        <div>25</div>
        <div>26</div>
        <div>27</div>
        <div>28</div>
        <div>29</div>
        <div>30</div>
        <div>31</div>

        <div class="next-date">1</div>
        <div class="next-date">2</div>
        <div class="next-date">3</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {}
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
  &__prev-date {
  }

  /* .calendar-days__next-date */

  &__next-date {
  }
  div {
    width: 12.74rem;
    height: 9.2rem;
    border: 1px solid #e9e9e9;
  }
}
.prev-date {
  /* .prev-date__date */

  &__date {
  }
}
.next-date {
}

hr {
  border: 1px solid #00416633;
  opacity: 0.2;
}
</style>
