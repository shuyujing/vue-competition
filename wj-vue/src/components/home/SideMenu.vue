<template>
  <el-aside>
      <el-menu
        default-active="1"
        @select="handleSelect"
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#5CB87A"
        style="width: 170px;min-height:400px;">
        <a href="#header-div">
          <el-menu-item index="1">
            <i class="el-icon-box"></i>
            <span slot="title">持仓查询</span>
          </el-menu-item>
        </a>
        <a href="#update-card">
          <el-menu-item index="2">
            <i class="el-icon-goods"></i>
            <span slot="title">产品查询</span>
          </el-menu-item>
        </a>
        <a href="#slogan">
          <el-menu-item index="3">
            <i class="el-icon-document"></i>
            <span slot="title">订单查询</span>
          </el-menu-item>
        </a>
        <a href="#about">
          <el-menu-item index="4">
            <i class="el-icon-shopping-cart-2"></i>
            <span slot="title">购买</span>
          </el-menu-item>
          </a>
      </el-menu>
  </el-aside>
</template>

<script>
  export default {
    data() {
          return {
            activeIndex:'',
          };
        },
    methods: {
      handleSelect(key, keyPath) {
        this.activeIndex=key;
        this.$emit('setActiveIndex', this.activeIndex)
      }
    },
    mounted(){
      console.log(1);
    }
  }
</script>

<style>
  a {
    text-decoration: none;
    color: inherit;
  }
  .el-menu-item i{
    color:#fff;
  }
</style>
