<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <tab-control class="tab-control" 
                 :titles="['流行', '新款', '精选']" 
                 @tabClick="tabClick"
                 ref="tabControl1"
                 v-show="isFixed"/>
    <scroll class="content" 
            ref="scroll" 
            @scroll="contentScroll" 
            @pullingUp="loadMore"
            :probe-type="3" 
            :pull-up-load="true">
      <home-swiper :banner="banner" @swiperImageLoad="swiperImageLoad"/>
      <home-recommend-view :recommend="recommend"/>
      <home-feature-view/>
      <tab-control :titles="['流行', '新款', '精选']" 
                   @tabClick="tabClick"
                   ref="tabControl2"/>
      <goods-list :goods="showGoods"/>
    </scroll>

    <back-top @click.native="backClick" v-show="isShowBackTop"/>   <!--监听组件的原生事件需要加.native修饰符-->
  </div>
</template>

<script>
import HomeSwiper from './childComps/HomeSwiper';
import HomeRecommendView from './childComps/HomeRecommendView';
import HomeFeatureView from './childComps/HomeFeatureView';

import TabControl from 'components/content/tabControl/TabControl';
import NavBar from 'components/common/navbar/NavBar';
import GoodsList from 'components/content/goods/GoodsList';
import Scroll from 'components/common/scroll/Scroll';
import BackTop from 'components/content/backTop/BackTop';

import {getHomeMultiData, getHomeGoods} from 'network/home';
import {debounce} from 'common/utils'


export default {
  name: 'Home',
  components: {
    HomeSwiper,
    HomeRecommendView,
    HomeFeatureView,
    NavBar,
    TabControl,
    GoodsList,
    Scroll,
    BackTop,
  },
  data() {
    return {
      banner: [],
      recommend: [],
      goods: {
        'pop': {page: 0, list: []},
        'new': {page: 0, list: []},
        'sell': {page: 0, list: []}
      },
      currentType: 'pop',
      isShowBackTop: false,
      isFixed: false,
      tabControlOffsetTop: 0,
      saveY: 0
    }
  },
  created() {
    this.getHomeMultiData();

    // 请求商品数据
    this.getHomeGoods('pop');
    this.getHomeGoods('new');
    this.getHomeGoods('sell');
  },
  activated() {
    this.$refs.scroll.scrollTo(0, this.saveY ,0);
    this.$refs.scroll.refresh();
  },
  deactivated() {
    this.saveY = this.$refs.scroll.getScrollY();
    console.log(this.saveY);
  },
  mounted() {
    // 图片加载完成后刷新scroll
    const refresh = debounce(this.$refs.scroll.refresh);   // 防抖
    this.$bus.$on('itemImageLoad', () => {
      refresh(); 
    });
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list
    }
  },
  methods: {
    /**
     * 事件请求相关的方法
     */
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = 'pop';
          break;
        case 1:
          this.currentType = 'new';
          break;
        case 2:
          this.currentType = 'sell'
          break;
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },
    backClick() {
      this.$refs.scroll.scrollTo(0, 0, 500);
    },
    contentScroll(position) {
      // 1.判断backTop是否显示
      this.isShowBackTop = (-position.y) > 1000;

      // 2.决定tabcontrol吸顶
      this.isFixed = (-position.y) > this.tabControlOffsetTop;
    },
    loadMore() {
      this.getHomeGoods(this.currentType);
    },
    swiperImageLoad() {
      this.tabControlOffsetTop = this.$refs.tabControl2.$el.offsetTop;
    },

    /**
     * 网络请求相关的方法
     */
    getHomeMultiData() {
      getHomeMultiData().then(res => {
        this.banner = res.data.banner.list;
        this.recommend = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page = page;

        this.$refs.scroll.finishPullUp();
      });
    }
  }
}
</script>

<style scoped>
  #home {
    /* padding-top: 44px; */
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background-color: var(--color-tint);
    color: #fff;

    /* position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9; */
  }

  .tab-control {
    position: relative;
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

  /* .content {
    height: calc(100% - 93px);
    overflow: hidden;
    margin-top: 44px;
  } */
</style>
