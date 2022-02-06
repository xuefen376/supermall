<template>
  <div class="shop-info">
    <div class="shop-top">
      <img :src="shop.shopLogo">
      <span class="title">{{shop.name}}</span>
    </div>
    <div class="shop-middle">
      <div class="shop-middle-item shop-middle-left">
        <div class="info-sells">
          <div class="sells-count">
            {{shop.cSells | sellCountFilter}}
          </div>
          <div class="sells-text">总销量</div>
        </div>
        <div class="info-goods">
          <div class="goods-count">
            {{shop.cGoods}}
          </div>
          <div class="goods-text">全部宝贝</div>
        </div>
      </div>
      <div class="shop-middle-item shop-middle-right">
        <table>
          <tr v-for="(item, index) in shop.score"
              :key="index">
            <td>{{item.name}}</td>
            <td class="score"
                :class="{'score-better': item.isBetter}">{{item.score}}</td>
            <td class="better"
                :class="{'better-more' : item.isBetter}"><span>{{item.isBetter
              ? '高' : '低'}}</span></td>
          </tr>
        </table>
      </div>
    </div>
    <div class="shop-bottom">
      <div class="enter-shop">进店逛逛</div>
    </div>
  </div>

</template>

<script>
export default {
  name: "DetailShopInfo",
  props: {
    shop: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  filters: {
    sellCountFilter (value) {
      let result = value;
      if (value > 10000) {
        result = (result / 10000).toFixed(1) + '万'
      }
      return result
    }
  }
}
</script>

<style scoped>
.shop-info {
  padding: 25px 8px;
  border-bottom: 5px solid #f2f5f8;
}
.shop-top {
  line-height: 45px;
  /*让元素垂直中心对*/
  display: flex;
  align-items: center;
}

.shop-top img {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  border: 1px solid rgb(0, 0, 0, 0.1);
}

.shop-top .title {
  margin-left: 10px;
  vertical-align: center;
}

.shop-middle {
  margin-top: 15px;
  display: flex;
  align-items: center;
}

.shop-middle-item {
  flex: 1;
}
</style>