<template>
    <div class="block" :class="{active:has_year}" :title="year + ' - ' + end"></div>
</template>
<script>
export default {
    props:['current','year'],
    computed:{
        end(){
            return this.year+10;
        },
        has_year(){
            if(this.current){
                if((this.year >= this.current.yob && this.year <= this.current.yod) || (this.end >= this.current.yob && this.end <= this.current.yod)){
                    return true;
                }
            }
            return false;
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
        box-sizing: border-box;
        width:2px;
        height:2px;
        display: inline-block;
        background: #fff;
        margin:14px;
    }
    .active{
        padding: 0px;
        background: yellow;
        width:20px;
        height:20px;
        margin:5px;
        display: inline-block;
    }
    @media screen and (max-width:720px){
    .block{
        width:2px;
        height:2px;
        margin:8px;
    }
        .active{
        width:15px;
        height:15px;
        margin:1px;
        }
    }


</style>
