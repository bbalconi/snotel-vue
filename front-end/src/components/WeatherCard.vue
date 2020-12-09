<template>
  <div id="WeatherCard">
    <div class="day-card" v-for="(location, index) in locations" :key="index">
      <div class='top-line'>
        <div class='button-wrap'>
          <button class="delete-button">X</button>
        </div>
        <div class='title-wrap'>
          <h1 class="location-name">{{ location.locationName }}</h1>
          <button class="edit-button">
            <i class="material-icons">mode_edit</i>
          </button>
        </div>
        <h3 class="header">{{ location.locationObject.daily.summary }}</h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WeatherCard',
  props: {
    locations: Array
  }
}
</script>

<style>
  .day-card {
    text-align: center;
    background: rgba(116, 116, 116, 0.1);
    max-width: 1600px;
    min-height: 400px;
    height: auto;
    width: auto;
    margin-top: 8px;
    margin-bottom: 20px;
    margin-left: auto;
    margin-right: auto;
    padding: .75em;
    border: 1px solid #9a6ae6;
    border-radius: 10px;
  }
  .location-name {
    color: #323031;
    margin-top: 0px;
    margin-bottom: 0px;
  }
  .edit-button {
    font-weight: bold;
    border-radius: 3px;
    color: white;
    width: 50px;
    height: 35px;
    background: #9a6ae6;
    font-size: 1.25em;
    border: 2px solid #9a6ae6;
    align-self: flex-end;
    margin-right: 7px;
    margin-left: 7px;
    font-family: Font Awesome 5 Solid;
  }
  .material-icons {
    color: 'white'; 
    font-weight: 'bold';
    margin-top: 3
  }
  .title-wrap {
    display: flex;
  }
  .top-line {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .button-wrap {
    display: flex;
    flex-wrap: row;
    align-self: flex-end;
  }
  .delete-button {
    font-weight: bold;
    border-radius: 3px;
    color: white;
    width: 50px;
    height: 35px;
    background: #ba7284;
    font-size: 1.25em;
    border: 2px solid #ba7284;
    align-self: flex-end;
  }
  .header {
    color: #323031;
    margin-top: 0px;
  }
</style>
