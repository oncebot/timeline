<template>
  <div id="app">
      <div class="container">
        <range-row v-for="start in starts" :start="start" :final="end"></range-row>
      </div>
  </div>
</template>

<script>
import RangeRow from '@/components/RangeRow';
export default {
  name: 'app',
  data(){
    return {
      start:-1000,
      end:2018,
    }
  },
  components: {
    RangeRow,
  },
  computed:{
    starts(){
        const years = [];
        let i = this.start;
        while (i<=this.end) {
          if(i==0){
            i=1;
          }
          years.push(i);
          i+=100;
        }
        return years;
    },
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.container{
  max-width: 900px;
  margin: auto;
}
</style>
