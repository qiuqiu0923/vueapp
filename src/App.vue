<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  mounted() {
    this.$axios.get('/api/cityList').then((res)=>{
       var city = res.data.data.cities;
       var zm_num = [];
       for(var i = 0; i < city.length; i++){
           console.log(city[i]);
           var filterzm = city[i].py.substring(0,1).toUpperCase();
           console.log(filterzm)
       }
    })
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
