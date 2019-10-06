<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab-wrapper">
      <tab :tabs="tabs" :initialIndex="initialIndex"></tab>
    </div>
  </div>
</template>

<script>
import Goods from "components/goods/goods";
import Ratings from "components/ratings/ratings";
import Seller from "components/seller/seller";
import VHeader from "components/v-header/v-header";
import Tab from "components/tab/tab";
import { getSeller } from "api";

// xiaoxin13pro

export default {
  name: "app",
  components: {
    Goods,
    Ratings,
    Seller,
    VHeader,
    Tab
  },
  data() {
    return {
      seller: {},
      initialIndex: 0
    };
  },
  created() {
    this._getSeller();
  },
  methods: {
    _getSeller() {
      getSeller({id: this.seller.id}).then(res => {
        this.seller = Object.assign({}, this.seller, res)
      });
    }
  },
  computed: {
    tabs() {
      return [
        {label: "商品", component: Goods, data: { seller: this.seller }},
        {label: "评价", component: Ratings, data: { seller: this.seller }},
        {label: "商家", component: Seller, data: { seller: this.seller }}
      ]
    }
  }
};
</script>
<style lang="stylus">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align center
  color: #2c3e50;
  // margin-top 60px
  overflow: hidden;

  .tab-wrapper {
    position: fixed;
    top: 136px;
    left: 0;
    right: 0;
    bottom: 0;
  }
}
</style>
