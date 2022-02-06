<template>
  <div class="detail">
    <detail-nav-bar />
    <scroll class="content">
      <detail-swiper :top-images="topImages" />
      <detail-base-info :goods="goodsInfo" />
      <detail-shop-info :shop="shopInfo" />
    </scroll>
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from './childComps/DetailSwiper'
import DetailBaseInfo from './childComps/DetailBaseInfo'
import DetailShopInfo from './childComps/DetailShopInfo'

import Scroll from 'components/common/scroll/Scroll'

import { getDetail, Goods } from "network/detail"

export default {
  name: 'Detail',
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    Scroll,
    DetailShopInfo
  },
  data () {
    return {
      iid: null,
      topImages: [],
      goodsInfo: {},
      shopInfo: {}
    }
  },
  created () {
    // 1.保存传入的iid
    this.iid = this.$route.params.iid
    // 2.根据iid请求详情数据
    getDetail(this.iid).then(res => {
      // 获取数据
      const data = res.data.result;

      // 1.从res中取出轮播图的信息
      this.topImages = data.itemInfo.topImages



      // 2.创建商品对象
      this.goodsInfo = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
      // 3.取出店铺的信息
      this.shopInfo = data.shopInfo
      console.log(data)
    })


  }

}
</script>

<style scoped>
.detail {
  height: 100vh;
  background-color: #fff;
  position: relative;
  z-index: 1;
}

.content {
  background-color: #fff;
  height: calc(100% - 44px);
}
</style>