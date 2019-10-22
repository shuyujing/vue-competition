<template>
<!--购买 -->
  <div>
  <el-form style='matgin-top:30px;'  ref="form" :model="infoData" label-width="140px">
  <el-row style='text-align:left;margin-left:5px;'>
    <el-col :span="8" :offset="2">
      <el-form-item label="产品代码：">
        <el-input v-model="infoData.productId" placeholder="产品代码" disabled></el-input>
      </el-form-item>
    </el-col>
    <el-col :span="8" :offset="2">
      <el-form-item label="产品风险等级：">
        <el-input v-model="infoData.productRiskLevel" placeholder="产品风险等级" disabled></el-input>
      </el-form-item>
    </el-col>
  </el-row>
  <el-row style='text-align:left;margin-left:5px;'>
    <el-col :span="8" :offset="2">
      <el-form-item label="产品大类：">
      <el-input v-model="infoData.productType" placeholder="产品大类" disabled></el-input>
      </el-form-item>
    </el-col>
    <el-col :span="8" :offset="2">
      <el-form-item label="募集总额：">
      <el-input v-model="infoData.productRaiseAmount" placeholder="募集总额" disabled></el-input>
      </el-form-item>
    </el-col>
  </el-row>
  <el-row style='text-align:left;margin-left:5px;'>
    <el-col :span="8" :offset="2">
      <el-form-item label="剩余额度：">
      <el-input v-model="infoData.productRemainAmount" placeholder="剩余额度" disabled></el-input>
      </el-form-item>
    </el-col>
    <el-col :span="8" :offset="2">
      <el-form-item label="产品名称：">
      <el-input v-model="infoData.productName" placeholder="产品名称" disabled></el-input>
      </el-form-item>
    </el-col>
  </el-row>
  <el-row style='text-align:left;margin-left:5px;'>
    <el-col :span="8" :offset="2">
      <el-form-item label="注册机构代码：">
      <el-input v-model="infoData.registrarCode" placeholder="注册机构代码" disabled></el-input>
      </el-form-item>
    </el-col>
    <el-col :span="8" :offset="2">
      <el-form-item label="注册登记机构名称：">
      <el-input v-model="infoData.registrarName" placeholder="注册登记机构名称" disabled></el-input>
      </el-form-item>
    </el-col>
  </el-row>
  <el-row>
    <el-col :span="12" :offset="4">
      <el-form-item>
        <el-button type="primary" @click="buy">去购买</el-button>
      </el-form-item>
    </el-col>
  </el-row>
  </el-form>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        infoData: {
          productId:'',
          productRiskLevel:'',
          productType:'',
          productRaiseAmount:'',
          productRemainAmount:'',
          productName:'',
          registrarCode:'',
          registrarName:'',
        },
      }
    },
    props:{
      initProductId:''
    },
    methods: {
        buy(){
          this.$emit('buyShow',
            {
              infoDetail:'infoDetail',
              productId:this.infoData.productId,
              customerId:this.$store.state.user.username
            }
          )
        },
        dataInit(){
          this.$axios
            .post('/eureka-provider-product/product/all', {
              productId: this.initProductId
            })
            .then(resp => {
                this.infoData = resp.data[0];
            })
            .catch(failResponse => {})
        }
    },
    mounted(){
      this.dataInit();
    }
  }
</script>
<style>
  .el-input.is-disabled .el-input__inner {
      background-color: #fff;
      border-color: #E4E7ED;
      color: #070;
      cursor: not-allowed;
  }
</style>
