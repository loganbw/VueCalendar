<template>
  <div class="calendarBox">
      
    <table id="calendarGrid" name="calendar">
      <tr v-for="(weekday, index) in DaysOfTheWeek" class="weekday">
        {{
          weekday
        }}
      </tr>
      <tr
        v-for="(box, index) in numberOfBoxes"
        :class="isActive ? 'boxActive' : 'box'"
        :key="boxKey"
        :id="index"
      >
        <td v-if="checkForStartDay(index) <= numberOfBoxes">
          {{ box - 2 }}
        </td>
      </tr>
    </table>
  </div>
  <p>
      {{firstDayTest}}
      </p>
</template>
<script>
export default {
    props:{
        firstDayTest: Date,
        daysInMonthTest: Number
    },
  inject: [
    "numberOfBoxes",
    "year",
    "DaysOfTheWeek",
    "firstDayOfMonth",
    "daystoMonth",
    "day",
  ],
  data() {
    return {
      numberOfBox: this.numberOfBoxes,
      thisYear: this.year,
      daysOfTheWeek: this.DaysOfTheWeek,
      inDateRange: false,
      days: [],
      isActive: false,
      today: this.day,
      boxClass: "box",
      boxClassActive: "boxActive",
      boxKey: 0,
    };
  },
  methods: {
    checkForStartDay(day) {
      this.setActiveDay(day);
      if (day >= this.firstDayTest.getDay() && day <= this.daysInMonthTest + 1) {
        return day;
      }
    },
    setActiveDay(day) {
      if (day === this.today) return (this.isActive = true);
      else {
        return (this.isActive = false);
      }
    },
  },
};
</script>
<style>
.boxActive {
  border: 2px solid black;
  padding: 3rem;
  background-color: red;
}
.boxActive:hover {
  background-color: green;
}
</style>
