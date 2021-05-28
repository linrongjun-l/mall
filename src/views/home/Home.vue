<template>
  <div id="home" >
      <!--头部导航栏-->
      <nav-bar class="home-nav">
        <template v-slot:center>
          <div>购物街</div>
        </template>
      </nav-bar>
    <scroll class="content02" ref="scroll" @scroll="contentScroll"  @pullingUp="loadMon"
            :probe-type="2"
            pull-up-load="true">
      <!--轮播图-->
      <home-swiper :banners="banner"></home-swiper>

      <!--推荐-->
      <recommend-view :recommends="recommends"></recommend-view>

      <!--本周流行-->
      <feature-view/>

      <!--tab-Controll-->
      <tab-control class="tab-control1" :titles="['流行','新款','精选']" @tabClick="tabClick" />

      <!--商品展示-->
      <goods-list :goods="goods[this.curType].list"></goods-list>
    </scroll>
    <!--返回到顶部按钮-->
    <back-top @click.native="backTopClick" v-show="isShowBackTop"/>
  </div>
</template>

<script>
  import HomeSwiper from "@/views/home/childComps/HomeSwiper";
  import RecommendView from "@/views/home/childComps/RecommendView";
  import FeatureView from "@/views/home/childComps/FeatureView";

  import NavBar from "@/components/common/navbar/NavBar";
  import TabControl from "@/components/content/tabcontrol/TabControl";
  import GoodsList from "@/components/content/goods/GoodsList";
  import Scroll from "@/components/common/scroll/Scroll";
  import BackTop from "@/components/content/backTop/BackTop";

  import {getHomeMultidata, getHomeGoods} from "@/network/home";



  export default {
    name: 'Home',
    components: {
      HomeSwiper,
      RecommendView,
      FeatureView,
      NavBar,
      TabControl,
      GoodsList,
      Scroll,
      BackTop,
    },
    data(){
      return {
        banner: '',
        recommends: '',
        curType: 'pop',
        goods: {
          'pop': {page: 0, list: []},
          'new': {page: 0,list: []},
          'sell': {page: 0,list: []}
        },
        isShowBackTop: false,
      }
    },
    created() {
      //1. 请求多个数据
      this.getHomeMultidata();

      //2. 获取data数据
      this.getHomeGoods('pop');
      this.getHomeGoods('new');
      this.getHomeGoods('sell');

    },
    methods: {
      /**
       * 网络请求相关函数
       */
      getHomeMultidata(){
        getHomeMultidata().then(res=>{
          this.banner = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getHomeGoods(type){
        let page = this.goods[type].page+1;
        getHomeGoods(type,page).then(res=>{
            this.goods[type].list.push(...res.data.list)
            this.goods[type].page+=+1;
            console.log(res.data.list);
        })
      },
      /**
       * 事件监听函数，监听TabControl组件
       * @param index
       */
      tabClick(index){
        switch (index){
          case 0:
            this.curType = 'pop';
            break;
          case 1:
            this.curType = 'new';
            break;
          case 2:
            this.curType = 'sell';
            break;
        }
      },
      backTopClick(){
        this.$refs.scroll.backTopClick(0,0);
      },
      contentScroll(position){
        this.isShowBackTop = (-position.y)>2000
      },
      loadMon(){
        console.log("45454")
        this.getHomeGoods(this.curType);
        this.$refs.scroll.finishPullUp();
      }
    }
  }

</script>


<style>
  #home {
    padding-top: 44px;
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
    text-align: center;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }

  .tab-control1 {
    position: sticky;
    top: 44px;
    z-index: 9;
  }

  .content02 {
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;

  }

  /*.content {*/
    /*height: calc(100% - 93px);*/
    /*overflow: hidden;*/
    /*margin-top: 44px;*/
  /*}*/
</style>
