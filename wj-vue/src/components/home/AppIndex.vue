<template>
  <div>
    <side-menu id="side-menu" v-on:setActiveIndex="setActiveIndex"></side-menu>
      <div class="home">
        <div id="header-div">
          <!-- 持仓查询-->
          <positionlist v-if="this.activeIndex==1"></positionlist>
          <!-- 产品查询-->
          <productlist v-if="this.activeIndex==2" v-on:infoShow="infoShow"></productlist>
          <!-- 订单查询 -->
          <orderlist v-if="this.activeIndex==3"></orderlist>
          <!-- 购买-->
          <buy v-if="this.activeIndex==4" :initProductId='initProductId'></buy>
          <!-- 详情-->
          <infoDetail v-if="this.activeIndex==5" :initProductId='initProductId' v-on:buyShow="buyShow"></infoDetail>
        </div>
      </div>
    </div>
</template>

<script>
  //持仓查询
  import positionlist from './positionlist'
  //产品查询
  import productlist from './productlist'
  //订单查询
  import orderlist from './orderlist'
  //购买
  import buy from './buy'
  //详情
  import infoDetail from './infoDetail'
  //
  import About from '@/components/common/About'
  import SideMenu from './SideMenu'
  export default {
    name: 'AppIndex',
    components: {positionlist, productlist, orderlist, About, buy, SideMenu,infoDetail},
    data() {
          return {
            activeIndex:'1',
            initProductId:''
          };
        },
    methods: {
      setActiveIndex(param){
          this.activeIndex=param;
          console.log(param);
      },
      infoShow(param){
        this.initProductId=param.row.productId;
        this.activeIndex='5'
      },
      buyShow(param){
        this.activeIndex='4'
      },
    }
  }
</script>

<style scoped>
  .home {
    width: 85%;
    margin-left: 180px;
    margin-top: 70px;
  }

  #header-div {
    padding: 15px;
    background-color: white;
    border-radius:5px;
    min-height:370px;
    /*background: url("../../assets/img/bg/bg3.jpg");*/
  }

  #side-menu {
    position: fixed;
    left:1%;
    top: 70px;
    text-align:left;
    padding:0px;
    border-radius:5px;
  }
</style>
