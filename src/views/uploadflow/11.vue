<template>
  <el-row justify="space-between" type="flex">
    <el-col :span="12" class="filter-button">
      <!-- 导入 -->
      <el-upload
        class="upload-demo inline-block"
        action="string"
        :http-request="httpRequest"
        :show-file-list="false"
        :before-upload="beforeAvatarUpload"
      >
        <el-button>导入</el-button>
      </el-upload>
      <el-button @click="exportExcel">导出</el-button>
      <el-button @click="download">下载</el-button>
    </el-col>
  </el-row>
</template>
<script>
export default {
  // name: "importFile",
  methods: {
    httpRequest(params) {
      // 上传我们需要传给后台两个必传参    file 和 filename  至于文件里面的内容后台处理就好
      const formdata = new FormData()
      formdata.append('File', params.file)
      formdata.append('FileName', params.file.name)
      // 这时候是打印不出来formdata的 只能通过 .get('File') 看是否append到formdata里
      this.$api.machine
        // 调用接口的话 都是封装后的 下面会贴一下我们的接口
        .importfacestatistics(formdata)
        .then(res => {
          // eslint-disable-next-line eqeqeq
          if (res.data.Code == 0) {
            this.$message.success(`成功导入${res.data.Data}条数据！`)
            this.getData()
            this.getData1()
          } else {
            this.$message.error(res.data.Msg)
          }
        })
        .catch(e => {
          this.$message.error(e)
        })
    },
    beforeAvatarUpload(file) {
      console.log(file)
      const isXls =
        file.type === 'application/vnd.ms-excel' ? true : file.type === 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'
      if (!isXls) {
        this.$message.error('上传的文件只能是xls以及xlsx格式!')
      }
      return isXls
    }
  },
  // 导入
  // 接口这部分大概也没什么要说的 无非就是 请求的方式 传的参数  以及 请求头
  importfacestatistics(formdata) {
    const baseUrl = window.config.API_HOST
    // eslint-disable-next-line no-undef
    return axios.request({
      url: `${baseUrl}/api/machines/importfacestatistics`,
      method: 'post',
      data: formdata,
      headers: { 'Content-Type': 'multipart/form-data' }
    })
  }

}
</script>
