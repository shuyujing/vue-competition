<template>
<!--产品列表查询 -->
  <div>
    <el-form :inline="true" :model="formInline" class="demo-form-inline">
      <el-form-item label="产品代码">
          <el-input v-model="formInline.productId" placeholder="产品代码"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="searchPROlist">查询</el-button>
      </el-form-item>
    </el-form>

    <el-table
        :data="tableData"
        stripe
        border
        style="width: 100%">
        <el-table-column label="操作" width="100">
          <template slot-scope="scope">
            <el-button
              type="primary"
              size="mini"
              @click="infoDetail(scope.$index, scope.row)">详情</el-button>
          </template>
        </el-table-column>
        <el-table-column prop="productId"  label="产品代码"  width="100">  </el-table-column>
        <el-table-column prop="productName"  label="产品名称"  width="120">  </el-table-column>
        <el-table-column prop="productRiskLevel"  label="产品风险等级"  width="120">  </el-table-column>
        <el-table-column prop="productType"  label="产品大类"  width="80">  </el-table-column>
        <el-table-column prop="productRaiseAmount"  label="募集总额"  width="120">  </el-table-column>
        <el-table-column prop="productRemainAmount"  label="剩余额度"  width="180">  </el-table-column>
        <el-table-column prop="registrarCode"  label="注册登记机构代码"  width="80">  </el-table-column>
        <el-table-column prop="registrarName"  label="注册登记机构名称"  width="120">  </el-table-column>
      </el-table>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        formInline: {
          productId: ''
        },
        tableData: []
      }
    },
    mounted: function() {
        this.searchPROlist()
    },
    methods: {
      searchPROlist () {
        var _this = this
        this.$axios
          .post('/eureka-provider-product/product/all', {
            productId: _this.formInline.productId
          })
          .then(resp => {
              _this.tableData = resp.data;
          })
          .catch(failResponse => {})
      },
      infoDetail(index,row){
        this.$emit('infoShow', {
          index:index,
          row:row
        })
      },

    }
  }
</script>
