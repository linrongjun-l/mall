<template>
  <div class="wrapper" ref="wrapper">
    <div class="content1">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScorll from "better-scroll"
export default {
  name: "Scroll",
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  data(){
    return {
      scroll: '',
    }
  },
  methods: {
    backTopClick(x=0,y=0,time=300) {
      this.scroll.scrollTo(x,y,time);
    },
    finishPullUp(){
      this.scroll.finishPullUp();
    }
  },
  mounted() {
    this.scroll = new BScorll(this.$refs.wrapper,{
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
      click: true
    })
    console.log(this.scroll)
    //监听滚动到什么位置
    this.scroll.on("scroll",(position)=>{
      this.$emit("scroll",position);
    })

    //监听下拉加载 更多
    this.scroll.on("pullingUp",()=>{
      this.$emit("pullingUp");
      //发送网络请求，请求更多页的数据

      //等数据请求完成，并且将新的数据展示出来后
      //this.scroll.finishPullUp(); //多次加载更多
    })
  }
}

</script>

<style scoped>

</style>