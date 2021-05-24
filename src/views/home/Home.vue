<template>
  <div id="home" class="wrapper">
      <!--头部导航栏-->
      <nav-bar class="home-nav">
        <template v-slot:center>
          <div>购物街</div>
        </template>
      </nav-bar>

    <!--轮播图-->
    <home-swiper :banners="banner"></home-swiper>

    <!--推荐-->
    <recommend-view :recommends="recommends"></recommend-view>

    <!--本周流行-->
    <feature-view/>

    <!--tab-Controll-->
    <tab-control class="tab-control1" :titles="['流行','新款','精选']" />
    <div>
      <ul>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
        <li>123</li>
      </ul>
    </div>
  </div>
</template>

<script>
  import NavBar from "@/components/common/navbar/NavBar";
  import TabControl from "@/components/content/tabcontrol/TabControl";

  import HomeSwiper from "@/views/home/childComps/HomeSwiper";
  import RecommendView from "@/views/home/childComps/RecommendView";
  import FeatureView from "@/views/home/childComps/FeatureView";

  import {getHomeMultidata} from "@/network/home";



  export default {
    name: 'Home',
    components: {
      NavBar,
      TabControl,
      HomeSwiper,
      RecommendView,
      FeatureView,
    },
    data(){
      return {
        banner: '',
        recommends: ''
      }
    },
    created() {
      //1. 请求多个数据
      getHomeMultidata().then(res=>{

        this.banner = res.data.banner.list;
        this.recommends = res.data.recommend.list;

      })
    }
  }
</script>


<style >
  #home {
    /*padding-top: 44px;*/
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
    top: 100px;
    z-index: 9;
  }

  .content {
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
