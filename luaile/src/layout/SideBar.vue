<template>
  <el-col>
    <el-menu :router="true"  default-active="2" class="el-menu-vertical-demo" unique-opened>
      <el-submenu v-for="data in DataList" :key="data.id" :index="data.path">
        <template slot="title">
          <i class="el-icon-location"></i>
          {{data.authName}}
        </template>
        <el-menu-item v-for="data2 in data.children" :key="data2.id" :index="'/'+data2.path">
          <i class="el-icon-menu"></i>
          {{data2.authName}}
        </el-menu-item>
      </el-submenu>
    </el-menu>
  </el-col>
</template>

<script>
export default {
  data () {
    return {
      DataList: []
    }
  },
  methods: {
    async getRightsList () {
      var rse = await this.$http.get(`/menus`, {})
      var { meta, data } = rse.data
      if (meta.status === 200) {
        this.DataList = data
      } else {
        this.$message.error(meta.msg)
      }
    }
  },
  mounted () {
    this.getRightsList()
  }
}
</script>

<style>
.el-aside {
  background-color: #fff;
}
.el-main {
  background-color: #d3dce6;
}
</style>
