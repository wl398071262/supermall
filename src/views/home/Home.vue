<template>
 <div id="home">
   <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
   <home-swiper :banners="banners"/>
   <recommend-view :recommends="recommends"></recommend-view>
 </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import HomeSwiper from './childComps/HomeSwiper'
  import RecommendView from './childComps/RecommendView'
  import {getHomeMultidata} from "network/home";


  export default {
    name: "home",
    components:{
      NavBar,
      HomeSwiper,
      RecommendView
    },
    data(){//保存请求到的数据
      return{
        banners:[],
        recommends:[]
      }
    },
    created() {//生命周期函数，请求网络数据
      //1.请求多个数据
      getHomeMultidata().then(res=>{
       /* this.result=res
        console.log(this.result);*/
       this.banners=res.data.banner.list;
       this.recommends=res.data.recommend.list;
      })
    }
  }
</script>

<style scoped>
.home-nav{
  background-color: var(--color-tint);
  color: #f2f2f2;
}
</style>
