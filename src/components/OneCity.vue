<template>
  <li>Город: {{oneCity.CityName}},{{oneCity.CityCountry}} <button @click="$emit('remove', oneCity)">X</button> </li>
  <li v-if="settings.checkedSky">Состояние неба: {{oneCity.Sky}}</li>
  <li v-if="settings.checkedTemperature">Температура: {{oneCity.Temperature}}<sup>°C</sup></li>
  <li v-if="settings.checkedSpeed">Скорость ветра: {{oneCity.Speed}} м/с </li>
  <li v-if="settings.checkedVisibility">Видимость: {{oneCity.Visibility}} м</li>
  <li v-if="settings.checkedPressure">Давление: {{oneCity.Pressure}} мм</li>
  <li><a v-bind:href="'detailed.html?'+ oneCity.CityID">Подробнее</a></li>
</template>

<script>
export default {
  name: "OneCity",
  props : {
    oneCity: {
      type: Object,
      required: true
    },
    settings: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
button {
  font-size: 1rem;
  font-weight: bold;
  letter-spacing: 0.1em;
  padding: 15px 20px;
  margin-left: 15px;
  border-radius: 5px;
  background: red;
  transition: background 0.3s ease-in-out;
  position: relative;
  float: right;
  color: black;
  border: none;
  outline: none;
}
</style>