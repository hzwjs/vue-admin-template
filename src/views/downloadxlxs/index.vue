<template>

  <el-form ref="form" :model="form" label-width="160px">
    <el-form-item
      label="下载文件起始时间"
    >
      <el-date-picker
        v-model="value1"
        type="daterange"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
      />
      <el-button type="primary" @click="onSubmit">按已选择时间下载文件</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  data() {
    return {
      pickerOptions: {
        shortcuts: [{
          text: '最近一周',
          onClick(picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 7)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近一个月',
          onClick(picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 30)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近三个月',
          onClick(picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 90)
            picker.$emit('pick', [start, end])
          }
        }]
      },
      value1: '',
      value2: ''
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
    }
  }
}
</script>

<style scoped>
.line{
  text-align: center;
}
/*.el-form-item{*/
/*  text-align: center;*/
/*}*/
</style>

