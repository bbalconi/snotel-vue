<template>
    <div>
      <p>{{coords.lat}} {{coords.lng}}{{coords.savedLat}} {{coords.savedLng}} {{coords.locationName}}</p>
      <button @click="saveLocation(coords)"/>
    </div>
</template>

<script>
export default {
  name: 'coords',
  props: ['coords'],
  methods: {
    async saveLocation(coords) {
      const response = await fetch('/api/getWeather', {
        method: 'POST',
        body: JSON.stringify({lat:coords.savedLat,lng:coords.savedLng}),
        headers: { 'Content-type': 'application/json; charset=UTF-8' }
      })
      const locData = await response.json()
      this.$emit("save:location", locData)
    }
  }
}
</script>