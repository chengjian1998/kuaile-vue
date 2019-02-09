<template>
  <el-card>
    <mybread firstnav="权限管理" lastnav="角色列表"/>
    <el-row>
      <el-col :span="8">
        <div>
          <el-input placeholder="请输入内容"  class="input-with-select">

            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </div>
      </el-col>
      <el-col :span="8">
          <div class="grid-content bg-purple-light">
          <el-button type="success">添加用户</el-button>
        </div>
      </el-col>
      <el-col :span="8">
          <div class="grid-content bg-purple"></div>
      </el-col>
    </el-row>
  </el-card>
</template>

<script>
export default {};
</script>

<style>
.el-breadcrumb {
  margin-bottom: 20px;
}
.bg-purple-light {
  padding-left: 10px;
}
</style>
