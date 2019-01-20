<template>
    <div class="row">
        <div class="title">{{ start_mod }}</div>
               <div class="flex-1">
                   <block-item v-for="year in range" :current="current" :year="year"></block-item>
               </div>
        <div class="title">{{ end_mod }}</div>
    </div>
</template>
<script>
import axios from 'axios';
import BlockItem from '@/components/BlockItem';
export default {
    props:['start','final','current'],
    components:{BlockItem},
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
        text-align: center;
        font-weight: 500;
    }
</style>
