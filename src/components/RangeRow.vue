<template>
    <div class="row">
        <div class="title">{{ start_mod }}</div>
               <div class="flex-1">
                <div class="block-row-holder">
                    <div class="block-row">
                        <block-item v-for="year in range" :current="current" :year="year"></block-item>
                    </div>
                </div>
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
        display: flex;
        justify-content: center;
        flex-direction: column;
    }
    @media screen and (max-width:600px){
        .row{
        background:#444;
        padding:12px;
        border-radius: 4px;
        margin: 6px;
        box-sizing: border-box;
        }
        .title{
            flex-basis: 100px;
        }
        .block-row{
            text-align: center;
        }
    }
    @media screen and (max-width:500px){
        .block-row{
            max-width:100px;
            margin: auto;
        }
    }
</style>
