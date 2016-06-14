<style lang="scss">
  $header-height: 100px;
  $day-size: 41px;

  .datepicker {
    position:absolute;
    top: 100%;
    width: 315px;
    z-index: 5;
    background-color: #fff;
    box-shadow: 0 14px 45px rgba(0, 0, 0, 0.25), 0 10px 18px rgba(0, 0, 0, 0.22);
  }

  .datepicker__header {
    background-color: #0097a7;
    color: #fff;
    padding: 20px;
    height: $header-height;
  }

  .datepicker__year {
    opacity: 0.7;
    margin-bottom: 10px;
    line-height: 16px;
  }

  .datepicker__date {
    font-size: 32px;
    line-height: 32px;
  }

  .datepicker__week {
    font-size: 12px;
    line-height: 12px;
    color: rgba(0, 0, 0, 0.8);
    padding: 0 14px;
  }

  .datepicker__weekdays {
    float: left;
    width: $day-size;
    text-align: center;
  }

  .datepicker__days {
    margin: 14px;
  }

  .datepicker__day {
    width: $day-size;
    height: $day-size;
    float: left;
    text-align: center;
  }
</style>

<template>
  <div class="datepicker">
    <div class="datepicker__header">
      <div class="datepicker__year">
        {{ year }}
      </div>
      <div class="datepicker__date">
        {{ date_formated }}
      </div>
    </div>
    <div class="datepicker__week">
      <div v-for="day in days" track-by="$index" class="datepicker__weekdays">
        {{ day }}
      </div>
    </div>
    <div class="datepicker__days">
      <div class="datepicker__day" v-bind:style="{width: (month.getWeekStart() * 41) + 'px'}">
      </div>
      <div class="datepicker__day" v-for="day in month.getDays()">
        {{ day.format('DD') }}
      </div>
    </div>
  </div>
</template>

<script>
import Month from '../modules/month'

export default {
  props: ['date'],
  data () {
    return {
      days: ['M', 'T', 'W', 'T', 'F', 'S', 'S'],
      month: new Month(this.date.month(), this.date.year())
    }
  },
  computed: {
    year () {
      return this.date.format('YYYY')
    },

    date_formated () {
      return this.date.format('dddd DD MMM')
    }
  }
}
</script>
