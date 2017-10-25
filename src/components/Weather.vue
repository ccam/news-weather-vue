<template>
  <div class="weather">
    <h2>Weather</h2>
    <div class="weatherContain">
     <div class="current">
       <h3>Current Weather</h3>
					<span>Tempature: {{current.main.temp}}°F</span><br>
          <span>Wind: {{current.wind.speed}} MPH</span><br>
          <span>Cloudiness: {{current.weather[0].main}}</span><br>
          <span>Humidity: {{current.main.humidity}} %</span><br>
          <span>Sunrise: {{sunriseTime}}</span><br>
          <span>Sunset: {{sunsetTime}}</span><br>
      </div>
      <div class="forecast">
          <div class="weekday">
            <h3>Monday</h3>
						<span>Forecast: {{forecastDesc[0]}}</span><br>
            <span>High Temp: {{forecast[0].temp.max}} °F</span><br>
            <span>Low Temp: {{forecast[0].temp.min}} °F </span><br>
            <span>Wind: {{forecast[0].speed}} MPH</span>
          </div>
          <div class="weekday">
            <h3>Tuesday</h3>
            <span>Forecast: {{forecastDesc[1]}}</span><br>
            <span>High Temp: {{forecast[1].temp.max}} °F</span><br>
            <span>Low Temp: {{forecast[1].temp.min}} °F </span><br>
            <span>Wind: {{forecast[1].speed}} MPH</span>

          </div>
          <div class="weekday">
            <h3>Wednesday</h3>
            <span>Forecast: {{forecastDesc[2]}}</span><br>
            <span>High Temp: {{forecast[2].temp.max}} °F</span><br>
						<span>Low Temp: {{forecast[2].temp.min}} °F </span><br>
            <span>Wind: {{forecast[2].speed}} MPH</span>

          </div>
          <div class="weekday">
            <h3>Thursday</h3>
            <span>Forecast: {{forecastDesc[3]}}</span><br>
            <span>High Temp: {{forecast[3].temp.max}} °F</span><br>
            <span>Low Temp: {{forecast[3].temp.min}} °F </span><br>
            <span>Wind: {{forecast[3].speed}} MPH</span>

          </div>
          <div class="weekday">
            <h3>Friday</h3>
            <span>Forecast: {{forecastDesc[4]}}</span><br>
            <span>High Temp: {{forecast[4].temp.max}} °F</span><br>
            <span>Low Temp: {{forecast[4].temp.min}} °F </span><br>
            <span>Wind: {{forecast[4].speed}} MPH</span>

          </div>
          <div class="weekday">
            <h3>Saturday</h3>
						<span>Forecast: {{forecastDesc[5]}}</span><br>
            <span>High Temp: {{forecast[5].temp.max}} °F</span><br>
            <span>Low Temp: {{forecast[5].temp.min}} °F </span><br>
            <span>Wind: {{forecast[5].speed}} MPH</span>

          </div>
          <div class="weekday">
            <h3>Sunday</h3>
            <span>Forecast: {{forecastDesc[6]}}</span><br>
            <span>High Temp: {{forecast[6].temp.max}} °F</span><br>
            <span>Low Temp: {{forecast[6].temp.min}} °F </span><br>
            <span>Wind: {{forecast[6].speed}} MPH</span>
            
          </div>

      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'weather',
  data () {
    return {
      current: {
        main: {},
        sys: {},
        wind: {},
        weather: {}
			},
      sunriseTime: '',
      sunsetTime: '',
      forecasteDate: '', // same as sunrise/set
		  forecast: '',
      forecastDesc: [] // fix this?
    }
  },
  methods: {
    convertSunrise () {
      for (let i = 0; i < 2; i++) {
        if( i === 1 ) {
          let time = new Date(this.current.sys.sunrise * 1000)
        let t = time.toLocaleString()
        this.sunriseTime = t.substring(11)
        } else {
          let time = new Date(this.current.sys.sunset * 1000)
        let t = time.toLocaleString()
        this.sunsetTime = t.substring(11)
        }
      }
    },
		upperDesc() {
			for (let i = 0; i < 7; i++) {
				let str = this.forecast[i].weather[0].description
				this.forecastDesc.push(str.charAt(0).toUpperCase() + str.slice(1))
			}
		}
  },
  mounted() {

    // this is the api call for the current weather
    axios.get('http://api.openweathermap.org/data/2.5/weather?id=5128638&units=imperial&APPID=141b6ad35e4f99e54fc551137b4db7e0 ')
    .then( response => {
        this.current = response.data
        this.convertSunrise()
				console.log(this.current)
      })

		//this is for the forecast
    axios.get('http://api.openweathermap.org/data/2.5/forecast/daily?id=5128638&units=imperial&APPID=141b6ad35e4f99e54fc551137b4db7e0')
    .then(res => {
      this.forecast = res.data.list
      this.upperDesc()
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.weatherContain {
  display: flex;
  justify-content: center;
	line-height: 1.5em;
}

.current, .forecast div {
  background-color :#667f6d;
	color: #f7f7f7;
  box-shadow: 3px 3px 3px #111;
  text-align: center;
  margin: 0 1vw;
	padding: 1vh 1vw;
}

.forecast {
  display: flex;
}
@media (max-width: 950px) {
  .weatherContain {
    flex-direction: column;
  }

  .current, .forecast div {
    margin: 1vh 10vw;
    width: 25vw;
  }

  .forecast {
    flex-wrap: wrap;
    
  }
}

@media (max-width: 1800px) {
  .weatherContain {
    flex-direction: column;
  }
  .forecast {
    flex-wrap: wrap;
  }
}
</style>
