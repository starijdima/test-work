<template>
  <div class="home">
    <datepicker v-bind:events="events"></datepicker>
  </div>
</template>

<script>
import datepicker from '../components/datepicker'
export default {
  name: 'HomeView',
  components: {
    datepicker
  },
  data(){
    return{
      events: [
        {id: 0, name: 'Записать на тренировку собаку', time: '18:00', day: '4', month: 'April', year: '2022', type: 'medium'},
        {id: 1, name: 'Закодить проект', day: '12', time: '12:00', month: 'April', year: '2022', type: 'high'},
        {id: 2, name: 'Закодить проект', day: '5', time: '11:00', month: 'April', year: '2022', type: 'high'},
        {id: 3, name: 'Сходить к врачу', time: '15:00', day: '5', month: 'April', year: '2022', type: 'low'},
        {id: 4, name: 'Какое-то длинное название мероприятия', time: '14:00', day: '16', month: 'April', year: '2022', type: 'medium'}
      ]
    }
  },
}
</script>
