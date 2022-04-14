<template>
  <div class="modal-container" id="modal-container" v-if="isVisible">
  <div class="modal" v-if="isVisible">
      <input type="checkbox" id="cbTemperature" name="cbTemperature" v-model="set.checkedTemperature">
      <label for="cbTemperature">Температура</label><br>
      <input type="checkbox" id="cbSky" name="cbSky" v-model="set.checkedSky">
      <label for="cbSky">Состояние неба</label><br>
      <input type="checkbox" id="cbSpeed" name="cbSpeed" v-model="set.checkedSpeed">
      <label for="cbSpeed">Скорость ветра</label><br>
      <input type="checkbox" id="cbPressure" name="cbPressure" v-model="set.checkedPressure">
      <label for="cbPressure">Давление</label><br>
      <input type="checkbox" id="cbVisibility" name="cbVisibility" v-model="set.checkedVisibility">
      <label for="cbVisibility">Видимость</label><br>
      <button id="close" @click="closeAndSaveOptions()">
        Закрыть настройки
      </button>
  </div>
  </div>
</template>

<script>
export default {
  name: "ModalSettings",
  methods: {
    closeAndSaveOptions() {
      this.$emit('closeSettings', this.set);
    }
  },
  props: {
    isVisible: {
      type: Boolean,
      required: true
    },
    curSets: {
      type: Object,
      required: true
    }
  },
  data()
  {
    return{
      set: {
        checkedSky: true,
        checkedTemperature: true,
        checkedSpeed: true,
        checkedVisibility: true,
        checkedPressure: true
      }
  }
  },
  created() {
    this.set = JSON.parse(localStorage.getItem('curSet'));
  }
}
</script>

<style scoped>
div.modal-container {
  background-color: rgba(0, 0, 0, 0.3);
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  display:flex;
  align-items: center;
  justify-content: center;
  pointer-events: auto;
  opacity: 1;
}

div.modal {
  background-color: #fff;
  border-radius: 5px;
  width: 600px;
  max-width: 100%;
  padding: 30px 50px;
  text-align: center;
}

</style>