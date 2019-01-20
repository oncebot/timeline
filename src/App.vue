<template>
  <div id="app">
      <div class="container">
        <range-row v-for="start in starts" :start="start" :final="end" :current="current"></range-row>
        <h1 class="text-center">
          {{ current_name }}
        </h1>
      </div>
  </div>
</template>

<script>
import RangeRow from '@/components/RangeRow';
import axios from 'axios';
export default {
  name: 'app',
  data(){
    return {
      start:-1000,
      end:2018,
      figures:[],
      next_index:null,
      current:null,
    }
  },
  components: {
    RangeRow,
  },
  methods:{
    set_current(){
      let index = this.next_index==null?0:this.next_index;
      if(!this.figures[index]){
        index = 0;
      }
        this.next_index = index+1;
        this.current = this.figures[index];
    },
  },
  computed:{
    current_name(){
      return this.current?this.current.name:'';
    },
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
    created(){
        axios.get('https://dev-util.edyst.com/challenge/person/'+this.start+'?end_yob='+this.end).then(response=>{
            this.figures = response.data;
            this.set_current();
            setInterval(()=>{
              this.set_current();
            },3000);
        }).catch((error)=>{
            console.log(error);
        });
    },
}
</script>

<style>
body{
  background: #333;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  margin-top: 60px;
}
.container{
  max-width: 700px;
  margin: auto;
}
.text-center{
  text-align: center;
}
</style>
