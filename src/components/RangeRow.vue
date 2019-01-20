<template>
    <div class="row">
        <div class="title">{{ start_mod }}</div>
               <div class="flex-1"><div v-for="year in range" class="block"></div></div>
        <div class="title">{{ end_mod }}</div>
    </div>
</template>
<script>
export default {
    props:['start','final'],
    computed:{
        end(){
            const end = this.start+99;
            return (end<this.final)?end:this.final;
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
</style>
