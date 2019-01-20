<template>
  <div id="app">
      
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {
  },
  computed:{
    chunks(){
        const start = -1000;
        const end = 2018;
        const chunkSize = 10;
        const years = [];
        let i = start;
        let temp = [];
        while (i<=end) {
          if(temp.length == 10){
            years.push(temp);
            temp = [];
          }else{
            temp.push(i);
            i+=10
          }
        }
      if(temp.length){
        years.push(temp);
      }
      if(!years[years.length-1].includes(end)){
        years[years.length-1].push(end);
      }
      return years;
    }
  },
  created(){
    console.log(this.chunks);
  }
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
