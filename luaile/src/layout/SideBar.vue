<template>
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
</template>

<script>
export default {
    data(){
        return{
            DataList: []
        }
    },
  methods: {
    async getRightsList() {
      var rse = await this.$http.get(`/menus`, {});
      var { meta, data } = rse.data;
      console.log(data);
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
.el-aside {
  background-color: #d3dce6;
  color: #333;
  text-align: center;
  line-height: 200px;
}
.el-aside {
  background-color: #fff;
}
.el-main {
  background-color: #d3dce6;
}
</style>
