<template>
  <div class="full-calendar-header">
    <div class="header-left">
      <slot name="header-left">
      </slot>
    </div>
    <div class="header-center">
      <span class="prev-month" @click.stop="goPrev">{{leftArrow}}</span>
        <picker  v-model="selectedMonth" @selected='selectMonth' dateFormat='YYYY年M月' :monthLabels='monthLabels'></picker>
      <span class="next-month" @click.stop="goNext">{{rightArrow}}</span>
    </div>
    <div class="header-right">
      <slot name="header-right">
      </slot>
    </div>
  </div>
</template>
<script type="text/babel">
  import dateFunc from './dateFunc'
  import moment from 'moment';
  import picker from 'vue-monthly-picker'
  export default {
    props : {
      currentMonth : {},
      titleFormat  : {},
      firstDay     : {},
      monthNames   : {},
      locale       : {},
    },
    data () {
      return {
        leftArrow  : '<',
        rightArrow : '>',
        selectedMonth:moment().format('YYYY年M月'),
        monthLabels:["1月", "2月", "3月", "4月", "5月", "6月", "7月", "8月", "9月", "10月", "11月", "12月"]
      }
    },
    computed: {
      title () {
        if (!this.currentMonth) return;
        return this.currentMonth.locale(this.locale).format('MMMM YYYY')
      }
    },
    methods : {
      goPrev () {
        var newMonth = moment(this.currentMonth).subtract(1, 'months').startOf('month');
        this.selectedMonth = newMonth;
        this.$emit('change', newMonth);
      },
      goNext () {
        var newMonth = moment(this.currentMonth).add(1, 'months').startOf('month');
        this.selectedMonth = newMonth;
        this.$emit('change', newMonth);
      },
      selectMonth(value){
        this.$emit('change', value);
      }
    },
    components:{
      picker
    }
  }
</script>
<style lang="scss">
.vue-monthly-picker{flex:1;}
.date-popover{position: absolute!important}
.header-center{position: relative;display: flex;}
.full-calendar-header{
  display: flex;
  align-items: center;
  .header-left,.header-right{
    flex:1;
  }
  .header-center{
    flex:3;
    text-align:center;
    .title{
      margin: 0 10px;
      cursor: pointer;
    }
    .prev-month,.next-month{
      cursor: pointer;
      flex:1;
    }
  }
}
</style>
