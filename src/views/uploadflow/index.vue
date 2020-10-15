<template>
  <div id="text">
    <el-form ref="form" :model="newData" label-width="160px" label-position="right" size="mini">
      <el-form-item label="上传文件" prop="name">
        <el-upload
          prop="File"
          ref="upload"
          multiple
          name="File"
          action=""
          :auto-upload="false"
          accept=".xls, .XLS,.xlsx, .XLSX,.xml, .XML"
          :http-request="httpRequest"
          :rules="[
      { required: true, message: '姓名不能为空'}
    ]">
          <el-button plain size="medium" type="info" round>选择要上传的文件</el-button>
<!--          <span slot="tip" class="el-upload__tip">&nbsp;&nbsp;&nbsp;只能上传xlxs/xml文件</span>-->
        </el-upload>
        <el-form-item>
        </el-form-item>
        <el-button type="primary" plain @click="newForm" size="medium" round>上传选定的文件<i class="el-icon-upload el-icon--right"></i></el-button>
<!--        <el-button type="info" plain @click="onCancel" size="medium" round>取消</el-button>-->
        <!--        <div slot="footer" class="dialog-footer">-->
<!--          <el-button type="primary" @click="newForm" size="mini">确 定</el-button>-->
<!--          <el-button @click="editDialog = false" size="mini">取 消</el-button>-->
<!--        </div>-->
      </el-form-item>
    </el-form>
  </div>
</template>
<script>

// import request from "@/Utils/request";

export default {
  data() {
    return {
      newData: {},
      file: []
    }
  },
  methods: {
    httpRequest(param) {
      this.file.push(param.file)// 一般情况下是在这里创建FormData对象，但我们需要上传多个文件，为避免发送多次请求，因此在这里只进行文件的获取，param可以拿到文件上传的所有信息
    },
    // 提交
    newForm() {
      var upData = new FormData()
      this.$refs.upload.submit()// 这里是执行文件上传的函数，其实也就是获取我们要上传的文件
      this.file.forEach(function(file) { // 因为要上传多个文件，所以需要遍历
        upData.append('file', file, file.name)
        // upData.append('file', this.file); //不要直接使用我们的文件数组进行上传，你会发现传给后台的是两个Object
      })
      upData.append('body', JSON.stringify(this.newData)) // 这里需要转换一下格式传给后台
      // eslint-disable-next-line no-undef
      request
        .post('http://localhost:12001/compare/uploadflow', upData)
        .then(function(response) {
          // eslint-disable-next-line eqeqeq,no-empty
          if (response.data.code == 200) {
          }
        })
        .catch(function(error) {
          console.log(error)
        })
    },
    onCancel() {
      this.$options.data() // 整个data全部重置
      // this.$message({
      //   message: 'cancel!',
      //   type: 'warning'
      // })
    }
  }
}
</script>
<style scoped>
#text{
  background: #fff;
  margin: 20px;
  padding: 20px
}
</style>
<style scoped>
.line{
  text-align: center;
}
.inline-block {
  display: inline-block;
}
</style>
