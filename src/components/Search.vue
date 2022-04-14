<template>
<section class="search">
        <form v-on:submit.prevent>
            <input v-model="this.City.CityName" id="nameOfCity" type="text" placeholder="Введите название города">
            <button type="submit" @click="createCity">+</button>
            <span class="msg"></span>
                    <button @click="$emit('removeAll')">X</button>
        <button @click="$emit('openSettings')"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-gear" viewBox="0 0 16 16">
            <path d="M8 4.754a3.246 3.246 0 1 0 0 6.492 3.246 3.246 0 0 0 0-6.492zM5.754 8a2.246 2.246 0 1 1 4.492 0 2.246 2.246 0 0 1-4.492 0z"/>
            <path d="M9.796 1.343c-.527-1.79-3.065-1.79-3.592 0l-.094.319a.873.873 0 0 1-1.255.52l-.292-.16c-1.64-.892-3.433.902-2.54 2.541l.159.292a.873.873 0 0 1-.52 1.255l-.319.094c-1.79.527-1.79 3.065 0 3.592l.319.094a.873.873 0 0 1 .52 1.255l-.16.292c-.892 1.64.901 3.434 2.541 2.54l.292-.159a.873.873 0 0 1 1.255.52l.094.319c.527 1.79 3.065 1.79 3.592 0l.094-.319a.873.873 0 0 1 1.255-.52l.292.16c1.64.893 3.434-.902 2.54-2.541l-.159-.292a.873.873 0 0 1 .52-1.255l.319-.094c1.79-.527 1.79-3.065 0-3.592l-.319-.094a.873.873 0 0 1-.52-1.255l.16-.292c.893-1.64-.902-3.433-2.541-2.54l-.292.159a.873.873 0 0 1-1.255-.52l-.094-.319zm-2.633.283c.246-.835 1.428-.835 1.674 0l.094.319a1.873 1.873 0 0 0 2.693 1.115l.291-.16c.764-.415 1.6.42 1.184 1.185l-.159.292a1.873 1.873 0 0 0 1.116 2.692l.318.094c.835.246.835 1.428 0 1.674l-.319.094a1.873 1.873 0 0 0-1.115 2.693l.16.291c.415.764-.42 1.6-1.185 1.184l-.291-.159a1.873 1.873 0 0 0-2.693 1.116l-.094.318c-.246.835-1.428.835-1.674 0l-.094-.319a1.873 1.873 0 0 0-2.692-1.115l-.292.16c-.764.415-1.6-.42-1.184-1.185l.159-.291A1.873 1.873 0 0 0 1.945 8.93l-.319-.094c-.835-.246-.835-1.428 0-1.674l.319-.094A1.873 1.873 0 0 0 3.06 4.377l-.16-.292c-.415-.764.42-1.6 1.185-1.184l.292.159a1.873 1.873 0 0 0 2.692-1.115l.094-.319z"/>
          </svg></button>
        </form>
        <div id="Time"></div>
</section>
</template>

<style scoped>
.search button,
.search input {
  border: none;
  background: none;
  outline: none;
  color: inherit;
}

.search input {
    -webkit-appearance: none;
}


.search{
    color: black;
}

.search form {
    position: relative;
    display: flex;
    align-items: center;
}

.search form input {
    font-size: 2rem;
    height: 40px;
    padding: 5px 5px 10px;
    border-bottom: 1px solid;    
}

.search form button {
    font-size: 1rem;
    font-weight: bold;
    letter-spacing: 0.1em;
    padding: 15px 20px; 
    margin-left: 15px;
    border-radius: 5px;
    background: red;
    transition: background 0.3s ease-in-out;
}

.search button {
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
    display: flex;
}
</style>

<script>
export default {

    data() {
        return {
          City: {
            CityName: "",
            CityCountry: "",
            Temperature: 0,
            Speed: 0,
            Sky: "",
            Pressure: 0,
            Visibility: 0,
            CityID: 0,
            id: 0
          }
        }
    },
    methods: {
        createCity() {
            const apiKey = "1d3881e0b2cddf04536dd417319cebf6";
            const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.City.CityName}&appid=${apiKey}&units=metric`;
            this.City.id = Date.now() + Math.random();
            fetch(url)
                .then(response => response.json())
                .then(data => {
                    this.City.CityID = data.id;
                    this.City.CityName = data.name;
                    this.City.Temperature = Math.round(data.main.temp);
                    this.City.CityCountry = data.sys.country;
                    this.City.Speed = data.wind.speed;
                    this.City.Sky = data.weather[0].description;
                    this.City.Pressure = data.main.pressure;
                    this.City.Visibility = data.visibility;

                    this.$emit('create', this.City);

                    this.City.CityName = '';
                })
                .catch(() => {
                  alert("Не правильное название города");
                });
        }
    }
}
</script>
