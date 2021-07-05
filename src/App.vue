<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search for the desired location..."/>
      </div>
      <div class="weather-root">
        <div class="info-container">
          <div class="location">Faridabad</div>
          <div class="date">Monday 5 July 2021</div>
        </div>
        <div class="weather-box">
          <div class="temp">43°c</div>
          <div class="weather">Sunny</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data (){
    return{
      api_key:'593210a225d49521802201d5fd34bdd2'
    }
  }
}
</script>

<style>
*{
  margin:0px;
  padding:0px;
  box-sizing: border-box;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#app{
  background:url('./assets/hotBg.jpeg');
  background-repeat:no-repeat;
  background-size:cover;
  background-position: top;
  height:100vh;
  transition:0.6s;
}
main{
  min-height:100vh;
  padding:2rem;
  background-image: linear-gradient(to bottom,rgba(0,0,0,0),rgba(0,0,0,0.75));
}
.search-box{
  width:100%;
  margin: 2rem 0px;
  display:flex;
  justify-content:center;
}
.search-bar{
  display: block;
  width: 100%;
  max-width: 800px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 1rem;
  
  color: #010101;
  font-size: 1.25rem;
  appearance: none;
  border:none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 0.5rem rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 1rem 0px 1rem 0px;
  transition: 0.6s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 1rem rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 0px 1rem 0px 1rem;
}
.info-container .location {
  color: #FFF;
  font-size: 2rem;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.info-container .date {
  color: #FFF;
  font-size: 1.25rem;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 0.75rem 1.55rem;
  color: #FFF;
  font-size: 8rem;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.5);
  border-radius: 1rem;
  margin: 2rem 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  cursor: default;
}
.weather-box .weather {
  color: #FFF;
  font-size: 3rem;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
