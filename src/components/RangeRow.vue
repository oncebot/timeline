<template>
    <div class="row">
        <div class="title">{{ start_mod }}</div>
               <div class="flex-1"><div v-for="year in range" class="block"></div></div>
        <div class="title">{{ end_mod }}</div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    props:['start','final','current'],
    methods:{
        has_year(year){
            if(this.current){
                console.log(this.current);
                if(this.current.yob >= year && this.current.yod <= year){
                    return true;
                }
            }
            return false;
        }
    },
    computed:{
        end(){
            const end = this.start+99;
            return (end<this.final)?end:this.final;
        },
        years(){
            let i = this.start;
            const end = this.end;
            const years = [];
            while(i<=end){  
                years.push(i);
                i++;
            }
            return years;            
        },
        range(){
            let i = this.start;
            const end = this.end;
            const range = [];
            while(i<=end){  
                if(i%10 == 0){
                range.push(i);
                }
                i++;
            }
            if(range[range.length-1]<this.final && end >= this.final){
                range.push(end);
            }
            return range;
        },
        start_mod(){
            return this.start < 0? 'BC '+Math.abs(this.start):'AD '+this.start; 
        },
        end_mod(){
            return this.end < 0? 'BC '+Math.abs(this.end):'AD '+this.end; 
        }
    },
}
</script>

<style>
    .row{
        display: flex;
    }
    .flex-1{
        flex:1;
    }
    .title{
        flex-basis: 200px;
    }
    .block{
        width:20px;
        height:20px;
        display: inline-block;
        margin:5px;
        background: #000;
    }
    .active{
        background: yellow;
    }
</style>
