<template>
<!--持仓查询 -->
  <div>
  <el-form :inline="true" :model="formInline" class="demo-form-inline">
  <el-form-item label="客户号">
    <el-input v-model="formInline.customerId" placeholder="客户号"></el-input>
  </el-form-item>
  <el-form-item label="产品代码">
      <el-input v-model="formInline.productId" placeholder="产品代码"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="searchPOSlist">查询</el-button>
  </el-form-item>
</el-form>

<el-table
      :data="tableData"
      stripe
      style="width: 100%">
      <el-table-column prop="customerId"  label="客户号"  width="180">  </el-table-column>
      <el-table-column prop="productId"  label="产品代码"  width="180">  </el-table-column>
      <el-table-column prop="totalVolume"  label="总持仓"  width="180">  </el-table-column>
      <el-table-column prop="onTheWayVol"  label="在途增"  width="180">  </el-table-column>
      <el-table-column prop="onTheWayAmt"  label="在途减"  width="180">  </el-table-column>
      <el-table-column prop="positionStatus"  label="持仓状态"  width="180">  </el-table-column>
    </el-table>

  </div>
</template>
<script>
  export default {
    data() {
      return {
        formInline: {
          customerId:this.$store.state.user.username,
          productId: ''
        },
        tableData: []
      }
    },
    mounted: function() {
        this.searchPOSlist()
    },
    methods: {
      searchPOSlist () {
        var _this = this
        this.$axios
          .post('/eureka-provider-user/user/Position/selectDynamic', {
            customerId: _this.formInline.customerId,
            productId: _this.formInline.productId
          })
          .then(resp => {
        //  alert("hello")
              _this.tableData = resp.data
          })
          .catch(ffailResponse => {})
      }
    }
  }
</script>
