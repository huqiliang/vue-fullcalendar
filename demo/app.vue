<template>
  <div>
  	<p>
  		Here is the demo of vue-fullcalendar2, no jquery fullcalendar.js required!
  	</p>
    <full-calendar  
      class="test-fc" 
      :events="fcEvents"
      first-day='1' 
      locale='zh'
      @changeMonth="changeMonth"
      @eventClick="eventClick"
      @dayClick="dayClick"
      @moreClick="moreClick">
        <template slot="fc-event-card" scope="p"  style='marginTop:30px'>
            <p>{{ p.event.title }}</p>
        </template>
    </full-calendar>
  </div>
</template>
<script>
let demoEvents = [
    {
      title    : 'Sunny 725-727',
      start    : '2017-12-25',
      end      : '2017-12-25',
      cssClass : 'family'
    },

  ];

export default {
	data () {
		return {
            name:'Sunny!',
            fcEvents : demoEvents
        }
	},
  methods : {
    'changeMonth' (start, end, current) {
      console.log('changeMonth', start.format('YYYY-MM-DD'), end.format('YYYY-MM-DD'), current.format('YYYY-MM-DD'))
    },
    'eventClick' (event, jsEvent, pos) {
       console.log('eventClick', event, jsEvent, pos)
    },
    'dayClick' (day, jsEvent) {
      console.log('dayClick', day, jsEvent)
    },
    'moreClick' (day, events, jsEvent) {
      console.log('moreCLick', day, events, jsEvent)
    }
  },
  components : {
    'full-calendar' : require('src/fullCalendar')
  }
}
</script>
<style lang='scss'>
  .app{
    color:green;
  }
</style>