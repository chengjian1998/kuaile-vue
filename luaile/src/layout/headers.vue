<template>
  <el-row>
    <el-col :span="2">
      <div class="grid-content bg-purple">
        <img src="@/assets/img/logo.png" alt>
      </div>
    </el-col>
    <el-col :span="20">
      <div class="grid-content bg-purple-light">
        <h2>电商后台管理系统</h2>
      </div>
    </el-col>
    <el-col :span="2">
      <div class="grid-content bg-purple">
        <a href="javascript:" @click="logout">退出</a>
      </div>
    </el-col>
  </el-row>
</template>

<script>
export default {
  data() {
    return {
      dialogVisible: false
    };
  },
  methods: {
    logout(done) {
      this.$confirm("确认关闭？", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消1",
        type: "warning"
      }).then(() => {
        window.localStorage.removeItem("token");
        this.$router.push("/login");
        this.$message({
          type: "success",
          message: "退出成功!"
        });
      });
    }
  }
};
</script>

<style>
/* 头部样式 */
.el-header {
  background-color: #b3c0d1;
  padding: 0;
  line-height: 60px;
}
.el-header .bg-purple-light {
  text-align: center;
  color: #fff;
}
.el-header .bg-purple a {
  color: #fff;
  text-decoration: none;
}
.el-header .bg-purple a:hover {
  color: red;
}
</style>
