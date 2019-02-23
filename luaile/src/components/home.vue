<template>
  <el-container>
    <el-header>
        <!-- 头部 -->
      <Headers/>
    </el-header>
    <el-container>
      <el-aside style="width: 200px;">
          <!-- 侧边栏 -->
      <SideBar/>
      </el-aside>
      <el-main>
          <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import Headers from '@/layout/headers.vue'
import SideBar from '@/layout/SideBar.vue'
export default {
  components: {
    Headers,
    SideBar
  },
  data () {
    return {}
  },
  methods: {},
  mounted () {}
}
</script>

<style>
.el-container {
  height: 100%;
}

* {
    margin: 0;
    padding: 0;
}
html, body, #app {
    height: 100%;
}
</style>
