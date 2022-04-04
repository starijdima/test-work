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
        {id: 0, name: 'test-1', date: '123', type: 1},
        {id: 1, name: 'test-2', date: '123', type: 2},
        {id: 2, name: 'test-3', date: '123', type: 3}
      ]
    }
  },
}
</script>
