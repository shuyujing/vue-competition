<template>
<!--购买 -->
  <div>
  <el-form style='matgin-top:30px;'  ref="form" :model="form" label-width="80px">
  <el-row style=''>
    <el-col :span="8" :offset="2">
    <el-form-item label="客户号">
      <el-input v-model="form.customerId" size='medium' :disabled='infoRoute'></el-input>
    </el-form-item>
    </el-col>
  </el-row>
  <el-row>
    <el-col :span="8" :offset="2">
      <el-form-item label="产品代码">
        <el-input  v-model="form.productId" size='medium' :disabled='infoRoute'></el-input>
      </el-form-item>
    </el-col>
  </el-row>
  <el-row>
    <el-col :span="8" :offset="2">
      <el-form-item label="交易金额">
        <el-input  v-model="form.transactionAmount" size='medium'></el-input>
      </el-form-item>
    </el-col>
  </el-row>
    <el-col :span="8" :offset="2">
      <el-form-item>
        <el-button type="primary" @click="buy">购买</el-button>
      </el-form-item>
    </el-col>
  </el-form>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        form: {
          customerId: this.$store.state.user.username,
          productId: '',
          transactionAmount: '',
          businessCode:''
        },
        infoRoute:false
      }
    },
    props:{
      initProductId:''
    },
    methods: {
      buy() {
        var _this = this
        this.$axios
          .post('/eureka-provider-control/transaction/buy', {
            customerId: _this.form.customerId,
            productId: _this.form.productId,
            transactionAmount: _this.form.transactionAmount,
            businessCode:'022'
          })
          .then(resp => {
            if(resp.data.orderSeq>0){
              this.$message({
                message: '购买成功！！！',
                type: 'success'
              });
            }else{
              this.$message.error('购买失败！！！');
            }
          })
          .catch(failResponse => {
            this.$message.error('购买失败！！！');
          })
      }
    },
    mounted(){
      if(this.initProductId){
        this.form.productId=this.initProductId;
        this.infoRoute=true;
      }
    }
  }
</script>
<style>

</style>
