<template>
  <div class="calendar">
    <div class="header">
      <a @click="lastMonth" class="btn">
        <svg class="arrow-switch" xmlns="http://www.w3.org/2000/svg" width="1024" height="1024" viewBox="0 0 1024 1024" fill="none">
        <path d="M685.248 104.704C697.246 116.706 703.986 132.981 703.986 149.952C703.986 166.923 697.246 183.198 685.248 195.2L368.448 512L685.248 828.8C696.906 840.871 703.357 857.037 703.211 873.818C703.065 890.598 696.335 906.65 684.468 918.516C672.602 930.383 656.55 937.113 639.77 937.259C622.989 937.405 606.823 930.954 594.752 919.296L232.704 557.248C220.706 545.246 213.966 528.971 213.966 512C213.966 495.029 220.706 478.754 232.704 466.752L594.752 104.704C606.754 92.7059 623.03 85.9657 640 85.9657C656.971 85.9657 673.246 92.7059 685.248 104.704V104.704Z" fill="black"/>
      </svg>
      </a>
      <p class="month">{{month}} <span v-if="year !== currentYear">{{year}}</span></p>
      <a @click="nextMonth" class="waves-effect waves-light btn">
        <svg class="arrow-switch arrow-switch-right" xmlns="http://www.w3.org/2000/svg" width="1024" height="1024" viewBox="0 0 1024 1024" fill="none">
          <path d="M685.248 104.704C697.246 116.706 703.986 132.981 703.986 149.952C703.986 166.923 697.246 183.198 685.248 195.2L368.448 512L685.248 828.8C696.906 840.871 703.357 857.037 703.211 873.818C703.065 890.598 696.335 906.65 684.468 918.516C672.602 930.383 656.55 937.113 639.77 937.259C622.989 937.405 606.823 930.954 594.752 919.296L232.704 557.248C220.706 545.246 213.966 528.971 213.966 512C213.966 495.029 220.706 478.754 232.704 466.752L594.752 104.704C606.754 92.7059 623.03 85.9657 640 85.9657C656.971 85.9657 673.246 92.7059 685.248 104.704V104.704Z" fill="black"/>
        </svg>
      </a>
    </div>
    <ul class="dates month">
      <li class="dow" v-for="dow in days">{{dow}}</li>
      <li v-for="empty in firstDayOfMonth" class="day last-month-day"></li>
      <li v-for="date in daysInMonth" @click="openday(date)"
          class="day" :class="{'today': date == initialDate && month == initialMonth && year == initialYear, 'past-day': date < initialDate && month == initialMonth && year == initialYear, 'weekend': true}">
        <div class="events">
          <div v-for="i in events" class="events-container">
            <p class="events-container-item" :class="i.type" v-if="i.day == date && i.month == month && i.year == year">{{i.time}} {{i.name}}</p>
          </div>
        </div>
        <span>{{date}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import moment from 'moment'
import arrow from '../assets/arrow.svg'
export default {
  props: {
    events: []
  },
  name: "datepicker",
  data(){
    return{
      today: this.moment(),
      dateContext: this.moment(),
      days: ['Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота', 'Воскресенье'],
      arrow,
      currentYear: moment().format('YYYY'),
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
      let firstDay = moment(t.dateContext).subtract((t.currentDate), 'days');
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
  },
}
</script>
