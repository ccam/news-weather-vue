<template>
  <div id="app">
    <header>
      <div>
        <img src="./assets/img/NYYStateSealdedass.png" alt="NY State Seal">
      </div>
      <h1>Ded Ass NYC</h1>
      <div>
        <img src="./assets/img/deadAssSeal.png" alt="NYC Seal">
      </div>
    </header>
		
    <news></news>
		<weather></weather>
  </div>
</template>

<script>
import News from './components/News'
import Weather from './components/Weather'

export default {
  name: 'app',
  components: {
    News,
    Weather
  }
}
</script>

<style>/* this will be used as global.css */
body {
  background-color: #333;
  color: #fff;
  font-family: Arial, Helvetica, sans-serif;
}

header {
  display: flex;
  justify-content: center;
}

header > div >img { 
  width: 150px;
  height: auto; 
}

header > h1 {
  width: 15vw;
  margin: 10vh 3vw 0 5vw;
  text-align: center;
}

h2 {
  font-weight: normal;
  text-align: center;
}

a {
  text-decoration: none;
  color: inherit;
}
/* Media Queries */


</style>
