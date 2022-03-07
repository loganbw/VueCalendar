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
</template>
<script>
export default {
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
      firstDay: this.firstDayOfMonth,
      daysInMonth: this.daystoMonth,
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
      if (day >= this.firstDay.getDay() && day <= this.daysInMonth + 1) {
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
