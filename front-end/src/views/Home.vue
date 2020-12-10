<template>
  <div class='home'>
    <google-map 
    class='map'
    @update:coords="setCoords"
    @save:coords="saveCoords"
    v-if="data" :locationData="data.locations"/>
    <coords 
    v-bind:coords="coords"
    @save:location="saveLocation"/>
    <weather-card @edit:card="sendEdit" @delete:day="deleteDay" v-bind:locations="data.locations"/>
  </div>
</template>

<script>
import WeatherCard from '@/components/WeatherCard.vue'
import GoogleMap from '@/components/GoogleMap.vue'
import Coords from '@/components/Coords.vue'

export default {
  components: { 
    GoogleMap,
    WeatherCard,
    Coords
  },
  name: 'home',
  data () {
    return {
      data: {},
      coords: {
        lat: 0,
        lng: 0,
        savedLat: 0,
        savedLng: 0,
        locationName: ''
      },
    }
  },
  methods: {
    logData() {
      this.data = this.$route.params.data
  }, async deleteDay(requestBody) {
      try {
        await fetch('/api/deleteDay', {
          method: 'POST',
          body: JSON.stringify(requestBody),
          headers: { 'Content-type': 'application/json; charset=UTF-8' },        
        })
        this.retrieveSavedLocations(this.$route.params.data._id)
      } catch(err) {
        console.log(err)
      }
    }, async retrieveSavedLocations(id) {
      const req = {id}
      try {
        const response = await fetch('/api/retrieveSavedLocations', {
          method: 'POST',
          body: JSON.stringify(req),
          headers: { 'Content-type': 'application/json; charset=UTF-8' },        
        })
        const data = await response.json()
        this.data.locations = data
      } catch(err) {
        console.log(err)
      }
    }, async sendEdit(newName, id) {
        const reqBody = {
          newLocationName: newName,
          _id: id,
          user_id: this.$route.params.data._id
          }
        try {
          await fetch('/api/updateLocationName', {
            method: 'PUT',
            body: JSON.stringify(reqBody),
            headers: { 'Content-type': 'application/json; charset=UTF-8' },        
          })
          this.retrieveSavedLocations(this.$route.params.data._id)
        } catch(err) {
          console.log(err)
        }
      }, setCoords(lat,lng) {
        this.coords.lat = lat
        this.coords.lng = lng
      }, async saveCoords(lat,lng) {
        this.coords.savedLat = lat
        this.coords.savedLng = lng
        let response = await fetch(`https://maps.googleapis.com/maps/api/geocode/json?latlng=${this.coords.savedLat}%2C${this.coords.savedLng}&language=en&key=AIzaSyA3ptyXyCL1xEpLtOr5rsls8BRzNt-Tgc0`)
        response = (await response.json()).results
        this.coords.locationName = response[0].formatted_address
        // switch (response) {
        //   case response.data.results["1"]:
        //     this.coords.locationName = response.data.results["1"].formatted_address
        //     break;
        //   case response.data.status === "ZERO_RESULTS":
        //     this.coords.locationName = ''
        //     break;
        //   default:
        //     this.coords.locationName = response.data.results["0"].formatted_address
        // }
      }, async saveLocation(locData) {
          const reqBody = {
            locationObject: locData,
            locationName: this.coords.locationName,
            _id: this.$route.params.data._id
          }
          await fetch('api/saveLocation', {
            method: 'POST',
            body: JSON.stringify(reqBody),
            headers: { 'Content-type': 'application/json; charset=UTF-8' },        
          })
          this.retrieveSavedLocations(this.$route.params.data._id)
      }
  },
  mounted () {
    this.logData()
  }
}
</script>

<style>
.home {
  margin: 0px auto; 
  padding: 0px 1em; 
  flex: 1 1
}
</style>