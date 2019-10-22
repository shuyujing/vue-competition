<template>
<!--订单查询 -->
  <div>
  <el-form :inline="true" :model="formInline" class="demo-form-inline">
    <el-form-item label="客户号">
        <el-input v-model="formInline.customerId" placeholder="客户号"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="searchORDERlist">查询</el-button>
    </el-form-item>
  </el-form>
  <el-table
      :data="tableData"
      stripe
      style="width: 100%">
      <el-table-column prop="orderSeq"  label="订单编号"  width="80">  </el-table-column>
      <el-table-column prop="createDate"  label="建单日期"  width="120">  </el-table-column>
      <el-table-column prop="createTime"  label="建单时间"  width="80">  </el-table-column>
      <el-table-column prop="transactionCode"  label="交易码"  width="80">  </el-table-column>
      <el-table-column prop="customerId"  label="客户编号"  width="120">  </el-table-column>
      <el-table-column prop="productId"  label="产品编号"  width="120">  </el-table-column>
      <el-table-column prop="transactionAmount"  label="交易金额"  width="150">  </el-table-column>
      <el-table-column prop="transactionVol"  label="交易份额"  width="150">  </el-table-column>
      <el-table-column prop="orderStatus"  label="订单状态"  width="80">  </el-table-column>
      <el-table-column prop="capitalStatus"  label="资金状态"  width="80">  </el-table-column>
    </el-table>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        formInline: {
          customerId:this.$store.state.user.username
        },
        tableData: []
      }
    },
    mounted: function() {
        this.searchORDERlist()
    },
    methods: {
      searchORDERlist () {
        var _this = this
        this.$axios
          .post('/eureka-provider-order/order/all', {
            customerId: _this.formInline.customerId
          })
          .then(resp => {
              _this.tableData = resp.data
          })
          .catch(failResponse => {})
      }
    }
  }
</script>
