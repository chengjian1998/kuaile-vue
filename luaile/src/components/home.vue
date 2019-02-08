<template>
  <el-container>
    <el-header>
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
            <a href="#">退出</a>
          </div>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside style="width: 200px;">
        <el-col>
          <el-menu default-active="2" class="el-menu-vertical-demo">
            <el-submenu v-for="data in DataList" :key="data.id" :index="data.path">
              <template slot="title">
                <i class="el-icon-location"></i>
                {{data.authName}}
              </template>
              <el-menu-item v-for="data2 in data.children" :key="data2.id" index="data2.path">
                <i class="el-icon-menu"></i>
                {{data2.authName}}
              </el-menu-item>
            </el-submenu>
          </el-menu>
        </el-col>
      </el-aside>
      <el-main>Main</el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
        DataList:[]
    };
  },
  methods: {
    async getRightsList() {
      var rse = await this.$http.get(`/menus`, {});
      var { meta, data } = rse.data;
      console.log(data)
      if (meta.status === 200) {
        this.DataList = data;
      } else {
        this.$message.error(meta.msg);
      }
    }
  },
  mounted(){
      this.getRightsList()
  }
};
</script>

<style>
.el-header,
.el-footer {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 60px;
}

.el-aside {
  background-color: #d3dce6;
  color: #333;
  text-align: center;
  line-height: 200px;
}

.el-main {
  background-color: #e9eef3;
  color: #333;
  text-align: center;
  line-height: 160px;
}

body > .el-container {
  margin-bottom: 40px;
}
.is-vertical {
  height: 100%;
}

.bg-purple-light h2 {
  color: #fff;
}
.bg-purple a {
  color: #fff;
}
.el-container {
  height: 100%;
}
.el-submenu__title {
  text-align: left;
}
</style>
