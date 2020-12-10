<template>
  <div>
    <GmapMap
      @mousemove="getCoords"
      @click="saveCoords"
      :center="{lat:center.lat, lng:center.lng}"
      :zoom="7"
      map-type-id="terrain"
      style="width: 500px; height: 300px">
        <GmapMarker
          :key="index"
          v-for="(m, index) in markers"
          :position="m.position"
        />
    </GmapMap>
  </div>
</template>

<script>
import Vue from 'vue'
import * as VueGoogleMaps from 'vue2-google-maps'
import {gmapApi} from 'vue2-google-maps'

Vue.use(VueGoogleMaps, {
  load: {
    key: 'AIzaSyCwZkE57pZxNg72QTmuajNgDQC_IK_XTy4',
    libraries: 'places'
  },
})

export default {
  name: 'GoogleMap',
  data() {
    return {
      markers: [],
      center: {
        lat: 45,
        lng: 110
      }
    }
  }, props: ['locationData'],
  methods: {
    getCoords(e) {
      let lat = e.latLng.lat()
      let lng = e.latLng.lng()
      lat = parseFloat(lat.toFixed(4))
      lng = parseFloat(lng.toFixed(4))
      this.$emit('update:coords', lat, lng)
    }, saveCoords(e) {
      let lat = e.latLng.lat()
      let lng = e.latLng.lng()
      lat = parseFloat(lat.toFixed(4))
      lng = parseFloat(lng.toFixed(4))
      this.$emit('save:coords', lat, lng)
    }, setMarkers() {
      const markerLocations = this.locationData
      let latArr = []
      let lngArr = []
      markerLocations.forEach((marker) => {
        const position = {
          lat: marker.locationObject.latitude,
          lng: marker.locationObject.longitude
        }
        latArr.push(position.lat)
        lngArr.push(position.lng)
        const label = marker.locationName
        this.markers.push({ position, label})
      })
      let average = (array) => array.reduce((a, b) => a + b) / array.length;
      this.center.lat = average(latArr)
      this.center.lng = average(lngArr)
    }
  }, created() {
      this.$nextTick(() => this.setMarkers())
  }, watch: {
      locationData: function () {
        this.markers = []
        this.setMarkers()
      }, markers: function () {
          const bounds = new gmapApi.maps.LatLngBounds()
          this.markers.forEach((marker) => {
            bounds.extend(marker.position)
          })
          this.$refs.gmap.$mapCreated.then((map) => {
            map.fitBounds(bounds);
          });
      }
  }
}
</script>