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
        :id="index"
        :key="index"
        ref="test"
        
      >
        {{
          displayDate(index)
        }}
      </tr>
    </table>
  </div>
</template>
<script>
let t = 0;
export default {
  props: {
    firstDayTest: Date,
    daysInMonthTest: Number,
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
      test: 0,
      resetDay: false,
    };
  },
  mounted() {
    this.loadDayArray();
    this.checkRef;
  },
  methods: {
    test1(index){
      console.log(index)
      if(index + 1 == this.today)
         return this.isActive = true;
      else return this.active = false
    },
    checkForStartDay(isday) {
      if (isday === this.today) return (this.isActive = true);
      else {
        return (this.isActive = false);
      }
    },
    loadDayArray() {
      for (let index = 0; index <= this.daysInMonthTest; index++) {
        this.days.push(index);
      }
      console.log(this.days.length);
    },
    updateDay() {
      return (this.day = this.day + 1);
    },
    logIt(item) {
      console.log(item);
    },
    displayDate(index) {
      //this.checkForStartDay(index)

      if (index >= this.firstDayTest.getDay()) {
        if (t < this.days.length - 1) {
          t++;
          return t;
        }
      }
    },
  },
  computed: {
    checkRef() {
      console.log(this.$refs.test[1].id);
      for (let index = 0; index < this.daysInMonthTest; index++) {
        if (this.$refs.test[index].id === this.day.toString())
          this.isActive = true;
        else this.isActive = false;
      }
    },
  },
  watch: {
    daysInMonthTest() {
      t = 0;
      this.resetDay = false;
      this.days = [];
      this.loadDayArray();
    },
  },
};
</script>
<style>
.boxActive {
  border: 2px solid black;
  padding: 2rem;
  background-color: red;
}
.boxActive:hover {
  background-color: green;
}
</style>
