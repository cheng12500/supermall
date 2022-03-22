<template>
  <div class="wrapper" ref="aaaa">
    <ul class="content">
    </ul>
  </div>
</template>

<script>
import BScroll from 'better-scroll'

  export default {
    name: "Category",
   data(){
     return{
       scroll:null
     }
   },
    created(){
      
    },
    mounted(){
      // console.log(this.$refs.aaaa);
      // console.log(document.querySelector('.wrapper'));
      this.scroll=new BScroll(document.querySelector('.wrapper'),{
        probeType:3,
        pullUpLoad:true
      })
      this.scroll.on('scroll',(position)=>{
        // console.log(position);
      })
      this.scroll.on('pullingUp',()=>{
        console.log('上拉加载更多');
      })
    }

  }
</script>

<style scoped>
  /* .wrapper{
    height: 150px;
    background-color: red;

    overflow: hidden; */
    /* overflow-y: scroll; */

  /* } */
</style>
