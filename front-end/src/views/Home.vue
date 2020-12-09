<template>
  <div class="about">
    <weather-card v-bind:locations="data.locations"/>
  </div>
</template>

<script>
import WeatherCard from '@/components/WeatherCard.vue'

export default {
  components: { 
    WeatherCard 
  },
  name: 'home',
  data () {
    return {
      data: {}
    }
  },
  methods: {
    logData() {
      this.data = this.$route.params.data

}
  },
  mounted () {
    this.logData()
  }
}
</script>