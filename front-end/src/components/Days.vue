<template>
  <div class="days">
    <div class="each-day" v-for="(day, i) in dayData" :key="i">
      <h2 class="title">{{dayConvertor(day, i)}}</h2>
      <h2 class="title">{{dateConvertor(day, i)}}</h2>
      <skycon :condition="day.icon" width="150" height="75"></skycon>
      <p class="summary">{{day.summary}}</p>
      <div>
          <p>Wind speed: <b class="wind">{{highLowData[i].windSpeed}} mph.</b><br/>
          Wind gusts: <b class="wind">{{highLowData[i].windGust}} mph.</b></p>
          <p>High: <b class="temp">{{highLowData[i].highTemp}}°F.</b></p>
          <p>Low: <b class="temp">{{highLowData[i].lowTemp}}°F.</b></p>
          <p v-if="day.precipType">Chance of {{day.precipType}}:<b class="temp">{{precip(day)}}%</b></p>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueSkycons from 'vue-skycon'

Vue.use(VueSkycons)

export default {
  name: 'days',
  data() {
    return {
      highLowData: []
    }
  },
  props: {
    dayData: Array
  },
  methods: {
    dateConvertor(day, index) {
      let d = new Date();
      let dd = d.getDate()+index;
      let mm = d.getMonth()+1;
      return `${mm}/${dd}`
    },
    dayConvertor(day, index) {
    let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    let d = new Date();
    let dayName = days[d.getDay() + index];
    return dayName
    },
    highLow(dayData) {
      dayData.forEach((day) => {
        let highTemp = day.apparentTemperatureHigh;
        let highRound = Math.round(highTemp);
        let lowTemp = day.apparentTemperatureLow;
        let lowRound = Math.round(lowTemp);
        let windDirection = `wi wi-wind from-${day.windBearing}-deg`
        let windSpeed = Math.round(day.windSpeed);
        let windGust = Math.round(day.windGust);

        const highLowObject = {
          highTemp,
          highRound,
          lowTemp,
          lowRound,
          windDirection,
          windSpeed,
          windGust
        }
        this.highLowData.push(highLowObject)
      })
    },
    precip(day){
      let probability = Math.floor(day.precipProbability*100); 
      return probability
    }
  },
  mounted() {
    this.highLow(this.dayData)
  }
}
</script>

<style>
  .each-day {
    background: rgba(156, 156, 145, 0.2);
    text-align: center;
    height: auto;
    width: 135px;
    padding-bottom: 0px;
    padding-top: 0px;
    padding-left: 1.5em;
    padding-right: 1.5em;
    margin-left: 5px;
    margin-right: 5px;
    margin-bottom: 5px;
    border: 1px solid #6228bf;
    border-radius: 5px;
  }
  .title {
    margin-top: .5em;
    color: #336699;
    margin-bottom: 0;
  }
  .days {
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
  }
  .summary {
    font-size: .9em;
    margin-bottom: .5em;
    margin-left: -12px;
    margin-right: -12px;
    font-weight: 525;
  }
  .text {
    font-size: 1em;
    color: black; 
  }
  .wind {
    color: #ba7284;
  }
  .temp {
    color: #336699;
  }
</style>