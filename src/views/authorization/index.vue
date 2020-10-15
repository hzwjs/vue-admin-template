<template>
  <div class="app-container" >
    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item
        label="产品类型"
        prop="resource"
        :rules="[
      { required: true, message: '产品类型不能为空'}
    ]">
        <el-radio-group v-model="form.resource">
          <el-radio label="车e贷" />
          <el-radio label="农e贷" />
        </el-radio-group>
      </el-form-item>
      <el-row>
        <el-col :span="8">
          <el-form-item
            label="姓名"
            prop="name"
            :rules="[
      { required: true, message: '姓名不能为空'}
    ]">
            <el-input v-model="form.name" />
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="8">
          <el-form-item
            label="身份证号"
            prop="idNo"
            :rules="[
      { required: true, message: '身份证号不能为空'}
    ]">
            <el-input v-model="form.idNo" maxlength="18" show-word-limit :validate-event="false" />
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="8">
          <el-form-item
            label="银行卡号"
            prop="cardNo"
            :rules="[
      { required: true, message: '银行卡号不能为空'},
      { type: 'number', message: '银行卡号必须为数字值'}
    ]">
            <el-input v-model="form.cardNo" maxlength="18" v-model.number="form.cardNo" />
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
      <el-col :span="8">
      <el-form-item
        label="手机号"
        prop="phoneNo"
        :rules="[
      { required: true, message: '手机号不能为空'},
      { type: 'number', message: '手机号必须为数字值'}
    ]">
        <el-input v-model="form.phoneNo" maxlength="18" v-model.number="form.phoneNo"/>
      </el-form-item>
      </el-col>
      </el-row>
      <el-row>
        <el-col :span="8">
          <el-form-item
            label="短信验证码"
            prop="phonecode"
            :rules="[
      { required: true, message: '短信验证码不能为空'},
      { type: 'number', message: '验证码必须为数字值'}
    ]">
            <el-input placeholder="请输入内容" v-model="form.phonecode" class="input-with-select" maxlength="18" v-model.number="form.phonecode">
              <el-button slot="append" plain type="primary" @click="sendMsg" >获取短信验证码</el-button>
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
        resource: '',
        name: '',
        idNo: '',
        cardNo: '',
        phoneNo: '',
        phonecode: ''
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate((valid) => {
        if (valid) {
          this.$message('submit!')
          // 向后台发送请求
        } else {
          // 就像用户提示发生错误的消息
        }
      })
    },
    sendMsg() {
      this.$message('submit!')
    },
    onCancel() {
      this.form = this.$options.data().form // 重置data中的 某个form表单
      // this.$message({
      //   message: 'cancel!',
      //   type: 'warning'
      // })
    }
  }
}
</script>

<style scoped>
.line{
  text-align: center;
}
.inline-block {
  display: inline-block;
}
</style>

