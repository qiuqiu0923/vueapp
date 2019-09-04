<template>
  <div id="app">

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
        var clitywrapper = [];
        for(var i = 0; i < city.length; i++){
            var cityszm = city[i].py.substring(0,1).toUpperCase();
            var tmp =  {index:cityszm,list:[{nm:city[i].nm,py:city[i].py}]};
            if( checkval( cityszm ) ){//新加index
                clitywrapper.push(tmp);
            }else{
              //追加index
                for(var j = 0; j < clitywrapper.length; j++){
                    if(clitywrapper[j].index === cityszm){
                        clitywrapper[j].list.push( {nm:city[i].nm,py:city[i].py} );
                    }
                }
            }
        };
        function checkval( cityszm ) {
            for(var t = 0; t < clitywrapper.length; t++){
                if(clitywrapper[t].index === cityszm){
                    return false;
                }
            }
            return true;
        };
        clitywrapper.sort((a,b)=>{
            if(a.index>b.index){
                return 1
            }else{
                return -1;
            }
        });console.log(clitywrapper)
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
