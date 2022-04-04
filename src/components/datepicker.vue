<template>
  <div class="calendar">
    <div class="header z-depth-2">
      <a @click="lastMonth" class="waves-effect waves-light btn"><i class="material-icons left">chevron_left</i>Last Month</a>
      <p>{{month}} {{year}}</p>
      <a @click="nextMonth" class="waves-effect waves-light btn"><i class="material-icons right">chevron_right</i>Next Month</a>
    </div>
    <ul class="dates month">
      <li class="dow" v-for="dow in days">{{dow}}</li>
      <li v-for="blank in firstDayOfMonth" class="day"></li>
      <li v-for="date in daysInMonth" @click="openday(date)"
          class="day" :class="{'today': date == initialDate && month == initialMonth && year == initialYear}">
        <span>{{date}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  props: {
    events: []
  },
  name: "datepicker",
  data(){
    return{
      today: this.moment(),
      dateContext: this.moment(),
      days: ['S', 'M', 'T', 'W', 'T', 'F', 'S']
    }
  },
  methods:{
    moment:moment,
    nextMonth: function () {
      let t = this;
      t.dateContext = moment(t.dateContext).add(1, 'month');
    },
    lastMonth: function () {
      let t = this;
      t.dateContext = moment(t.dateContext).subtract(1, 'month');
    }
  },
  computed: {
    year: function () {
      let t = this;
      return t.dateContext.format('YYYY');
    },
    month: function () {
      let t = this;
      return t.dateContext.format('MMMM');
    },
    daysInMonth: function () {
      let t = this;
      return t.dateContext.daysInMonth();
    },
    currentDate: function () {
      let t = this;
      return t.dateContext.get('date');
    },
    firstDayOfMonth: function () {
      let t = this;
      let firstDay = moment(t.dateContext).subtract((t.currentDate - 1), 'days');
      return firstDay.weekday();
    },
    //Previous Code Above
    initialDate: function () {
      let t = this;
      return t.today.get('date');
    },
    initialMonth: function () {
      let t = this;
      return t.today.format('MMMM');
    },
    initialYear: function () {
      let t = this;
      return t.today.format('YYYY');
    }
  }
}
</script>
