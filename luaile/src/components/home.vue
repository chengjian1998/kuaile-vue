<template>
  <el-container>
    <el-header>
      <Headers/>
    </el-header>
    <el-container>
        <SideBar/>
      <el-main>Main</el-main>
    </el-container>
  </el-container>
</template>

<script>
import Headers from "@/layout/headers.vue";
import SideBar from "@/layout/SideBar.vue";
export default {
  components: {
    Headers,
    SideBar
  },
  data() {
    return {
    };
  },
  methods: {

  },
  mounted() {
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
