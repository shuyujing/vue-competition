<template>
  <div class='header-menu'>
    <el-menu
      :default-active="'/index'"
      mode="horizontal"
      @select="handleSelect"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#5CB87A"
      style="min-width: 1200px;border-radius:5px;">
      <el-menu-item v-for="(item,i) in navList" :key="i" :index="item.name" style="margin-left:5px;">
        {{ item.navItem }}
      </el-menu-item>
      <a href="#nowhere" class='more-actions' >更多功能</a>
      <i class="el-icon-menu" style="float:right;font-size: 45px;color: #5CB87A;padding-top: 8px"></i>
      <span class='header-title'>O C T O P U S</span>
      <el-input
        placeholder="快速搜索..."
        prefix-icon="el-icon-search"
        size="medium"
        style="width: 300px;position:absolute;margin-top: 12px;right: 13%"
        v-model="keywords">
      </el-input>
    </el-menu>
  </div>
</template>

<script>
  export default {
    name: 'NavMenu',
    data () {
      return {
        navList: [
          {name: '/index', navItem: '首页'},
          {name: '/jotter', navItem: '基金'},
          {name: '/library', navItem: '代销理财'},
          {name: '/admin', navItem: '个人中心'}
        ],
        keywords: ''
      }
    },
    computed: {
      hoverBackground () {
        return '#ffd04b'
      }
    },
    methods: {
      handleSelect (key, keyPath) {
        console.log(key, keyPath)
      }
    }
  }
</script>

<style scoped>
  a{
    text-decoration: none;
  }

  span {
    pointer-events: none;
  }
  .header-title{
    position: absolute;
    font-size: 32px;
    font-weight: bold;
    display:block;
    width:100%;
    height:64px;
    line-height:64px;
    color: #fafafa;
  //  letter-spacing: 0;
  //  text-shadow: 0px 1px 0px #999, 0px 2px 0px #888, 0px 3px 0px #777, 0px 4px 0px #666, 0px 5px 0px #555, 0px 6px 0px #444, 0px 7px 0px #333, 0px 8px 7px #001135
  }
  .more-actions{
    color: #fff;
    float: right;
    padding: 20px;
  }
  .more-actions:hover{
    color:#5CB87A;
  }
  .header-menu{
    width:98%;
    position:fixed;
    left:1%;
    top:0px;
    z-index:999;
  }
</style>
