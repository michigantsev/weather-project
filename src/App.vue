<script setup>
import CityList from './components/CityList.vue'
import Search from './components/Search.vue'
import ModalSettings from "./components/ModalSettings.vue";

</script>

<template>
  <ModalSettings
      v-bind:isVisible=this.isSettingsVisible
      v-bind:curSets=this.currentSettings
      @closeSettings="closeSettings"/>
<Search 
@create="createCity"
@removeAll="removeAllCities"
@openSettings="openSettings"/>
<CityList
v-bind:cities="arrayOfCities"
v-bind:settings="currentSettings"
@remove ="removeCity" />
</template>

<style>
body {
    font: 1rem/1.3 "Roboto", sans-serif;
    background-image: url(https://fullhdoboi.ru/wp-content/uploads/_ph/6/942552018.jpg);
    color: #1e2432;
    padding: 50px;
}
</style>
<script>
export default {
    components: {
        Search,
        CityList,
        ModalSettings
    },
    data() {
        return {
            arrayOfCities: [],
            isSettingsVisible: false,
            currentSettings: null
        }
    },
    methods: {
        createCity(city)
        {
          const newCity = {
            CityName: city.CityName,
            CityCountry: city.CityCountry,
            Temperature: city.Temperature,
            Speed: city.Speed,
            Sky: city.Sky,
            Pressure: city.Pressure,
            Visibility: city.Visibility,
            CityID: city.CityID,
            id: city.id
          }

          this.arrayOfCities.push(newCity);

          localStorage.setItem("arrayOfCities", JSON.stringify(this.arrayOfCities));
        },

        removeCity(city){
          this.arrayOfCities = this.arrayOfCities.filter(p => p.id !== city.id);

          localStorage.setItem("arrayOfCities", JSON.stringify(this.arrayOfCities));
        },

        removeAllCities(){
          this.arrayOfCities = [];

          localStorage.setItem("arrayOfCities", JSON.stringify(this.arrayOfCities));
        },

        closeSettings(set){
          this.isSettingsVisible = false;
          const settings = {
            checkedSky: set.checkedSky,
            checkedTemperature: set.checkedTemperature,
            checkedSpeed: set.checkedSpeed,
            checkedVisibility: set.checkedVisibility,
            checkedPressure: set.checkedPressure
          }

          this.currentSettings = settings;

          localStorage.setItem('curSet', JSON.stringify(settings));
        },

        openSettings(){
          this.isSettingsVisible = true;
        }
    },
  created() {
      if(localStorage.getItem('curSet') != null)
        this.currentSettings = JSON.parse(localStorage.getItem('curSet'));
      else
        this.currentSettings = {
          checkedSky: true,
          checkedTemperature: true,
          checkedSpeed: true,
          checkedVisibility: true,
          checkedPressure: true
        };

    if(localStorage.getItem("arrayOfCities") != null)
        this.arrayOfCities = JSON.parse(localStorage.getItem("arrayOfCities"));
  }
}
</script>
