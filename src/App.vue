<script>
import CalendarBox from "./components/CalendarBox.vue";
const today = new Date();
const day = today.getDate();
const dOTW = today.getDay();
const month = today.getMonth();
const year = today.getFullYear();

const getFirstDayOfMonth = (year, month) => {
  return new Date(year, month, 1);
};
const daysInMonths = [
  31,
  (year % 4 == 0 && year % 100 != 0) || year % 400 == 0 ? 29 : 28,
  31,
  30,
  31,
  30,
  31,
  31,
  30,
  31,
  30,
  31,
];
export default {
  components: {
    CalendarBox,
  },
  data() {
    return {
      months: [
        "January",
        "Feburary",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "Setemper",
        "October",
        "November",
        "December",
      ],
      DaysOfTheWeek: [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ],
      day: day,
      month: month,
      year: year,
      dotw: dOTW,
      daysInMonths: daysInMonths,
      todayActive: false,
      monthString: "",
      weekString: [],
      firstDayOfMonth: getFirstDayOfMonth(year, month),
      numberOfBoxes: 42,
      daystoMonth: daysInMonths[month],
    };
  },
  mounted() {
    this.UpdateAndShowMonth();
  },
  methods: {
    UpdateAndShowMonth() {
      this.monthString = this.months[this.month];
      console.log(day);
    },
    previousMonth() {
      if (this.month > 0) {
        this.month--;
        this.monthString = this.months[this.month];
        this.daystoMonth = this.daysInMonths[this.month];
        this.firstDayOfMonth = getFirstDayOfMonth(this.year, this.month);
      } else {
        this.month = 11;
        this.monthString = this.months[this.month];
        this.daystoMonth = this.daysInMonths[this.month];
        this.year--;
      }
    },
    nextMonth() {
      if (this.month < 11) {
        this.month++;
        this.monthString = this.months[this.month];
        this.firstDayOfMonth = getFirstDayOfMonth(this.year, this.month);
        this.daystoMonth = this.daysInMonths[this.month];
      } else {
        this.month = 0;
        this.monthString = this.months[this.month];
        this.daystoMonth = this.daysInMonths[this.month];
        this.year++;
      }
    },
    highlightToday(days) {
      if (days == this.day && month == this.month) {
        this.todayActive = true;
        return { boxActive: this.todayActive };
      }
    },
    log(item) {
      console.log(item);
    },
  },
  computed: {},
  provide() {
    return {
      numberOfBoxes: this.numberOfBoxes,
      year: this.year,
      DaysOfTheWeek: this.DaysOfTheWeek,
      firstDayOfMonth: this.firstDayOfMonth,
      daystoMonth: this.daystoMonth,
      day: this.day,
    };
  },
  props:["first-day-test", "days-in-month-test", "this-month" , "this-year"]
};
</script>

<template>
  <header>
    <h1 class="monthName">{{ monthString }}</h1>
    <button @click="previousMonth" class="navMonthLeft btn">Past Month</button>
    <button @click="nextMonth" class="navMonthRight btn">Next Month</button>
    <h2 class="year">{{ year }}</h2>
  </header>
  <main>
    <CalendarBox :first-day-test="this.firstDayOfMonth"  :days-in-month-test=" this.daystoMonth" :this-month="this.month" :this-year="this.year"/>
  </main>
</template>

<style>
@import "./assets/base.css";

#app {
  margin: 0 auto;
  font-weight: normal;
}
#calendarGrid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 10px;
  grid-auto-rows: minmax(100px, auto);
  margin-top: 10%;
  margin-bottom: 10%;
}
.weekday {
  text-align: center;
  margin-top: 70%;
  font-weight: bold;
}
.box {
  border: 2px solid black;
  padding: 1rem;
  background-color: grey;
}
.box:hover {
  background-color: hsla(160, 100%, 37%, 0.2);
}

.monthName {
  text-align: center;
  padding-top: 5%;
  margin-bottom: -5%;
}
.navMonthLeft {
  float: left;
  position: relative;
  top: 15%;
  left: 10%;
  margin-top: 2%;
}
.navMonthRight {
  float: right;
  position: relative;
  top: 5%;
  right: 8%;
  margin-top: 2%;
}
.year {
  text-align: center;
  margin-top: 5%;
  margin-bottom: -15%;
}
header {
  line-height: 1.5;
  display: inline !important;
  text-align: center;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
