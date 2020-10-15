<template>
  <div class="app-container">
    <el-form ref="form" :model="form" label-width="120px">

      <el-form-item label="产品类型">
        <el-radio-group v-model="form.resource">
          <el-radio label="车e贷" />
          <el-radio label="农e贷" />
        </el-radio-group>
      </el-form-item>
      <el-row>
        <el-col :span="8">
          <el-form-item label="姓名">
            <el-input v-model="form.phoneNo" />
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="8">
          <el-form-item label="身份证号">
            <el-input v-model="form.phoneNo" />
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="8">
          <el-form-item label="银行卡号">
            <el-input v-model="form.phoneNo" />
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
      <el-col :span="8">
      <el-form-item label="手机号">
        <el-input v-model="form.phoneNo" />
      </el-form-item>
      </el-col>
      </el-row>
      <el-row>
        <el-col :span="8">
          <el-form-item label="短信验证码">
            <el-input placeholder="请输入内容" v-model="input3" class="input-with-select">
              <el-button slot="append" >获取短信验证码</el-button>
            </el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">开通协议支付</el-button>
          <el-button  type="info" @click="onCancel">重置所有数据</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      }
    }
  },
  methods: {
    onSubmit() {
      this.$message('submit!')
    },
    onCancel() {
      this.$message({
        message: 'cancel!',
        type: 'warning'
      })
    }
  }
}
</script>

<style scoped>
.line{
  text-align: center;
}
</style>

