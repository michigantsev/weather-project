<template>
<div class="city" v-for="city in cities">
    <OneCity v-bind:oneCity="city" :key="city.id" @remove="$emit('remove', city)" v-bind:settings="settings"/>
</div>
</template>

<style scoped>
div.city {
  margin: 10px 20px 30 40px;
  padding: 10px 20px 30 40px;
  border: solid 4px;
  border-color: aquamarine;
  float: left;
  background-color: rgba(104, 224, 184, 0.5);;
  background-repeat: no-repeat;
  font:700;
  font-size: 36px;
  color: red;
  display:table-cell;
}

</style>

<script>
import OneCity from "./OneCity.vue";
export default {
    props: {
        cities: {
            type: Array,
            required: true
        },
        settings: {
          type: Object,
          required: true
        }
    },
  components: {
      OneCity
  }
}
</script>
