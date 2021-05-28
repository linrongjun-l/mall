<template>
  <div class="wrapper">
    <ul>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
    </ul>
  </div>
</template>

<script>
import BScroll from "better-scroll";
  export default {
    name: 'Category',
    data(){
      return {
        scroll: ''
      }
    },
    mounted() {
      //默认情况下BScroll是不可以实时的监听滚动的位置
      //probe 侦测
      //0，1都不是侦测实时的位置
      // 2 ： 在手指滚动的过程中侦测，手指离开后的惯性滚动不侦测
      // 3 ：只要是滚动都侦测
      this.scroll = new BScroll(document.querySelector('.wrapper'),{
        probeType: 0,
        click: true, //在scroll中click点击失效，需要设置true
        pullUpLoad: true //上拉加载更多
      })

      //第一个参数是监听的类型(scroll滚动)
      this.scroll.on("scroll",(position)=>{
        console.log(position);
      })

      //上拉加载更多
      this.scroll.on("pullingUp",()=>{
        console.log("上拉加载跟多。。。")
        //发送网络请求，请求更多页的数据

        //等数据请求完成，并且将新的数据展示出来后
        this.scroll.finishPullUp(); //多次加载更多
      })
    }
  }
</script>

<style scoped>
  .wrapper {
    height: 150px;
    background-color: red;

    overflow: hidden;
    /*overflow-y: scroll;*/
  }
</style>
