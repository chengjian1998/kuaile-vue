<template>
  <el-card>
    <mybread firstnav="权限管理" lastnav="角色列表"/>
    <el-row>
      <el-col :span="8">
        <div>
          <el-input placeholder="请输入内容" class="input-with-select">
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="grid-content bg-purple-light">
          <el-button type="success" @click="dialogFormVisible=!dialogFormVisible">添加用户</el-button>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="grid-content bg-purple"></div>
      </el-col>
    </el-row>

    <!-- 表格 -->
    <el-table :data="tableData" border style="width: 100%">
      <el-table-column type="index"></el-table-column>
      <el-table-column prop="username" label="姓名" width="180"></el-table-column>
      <el-table-column prop="email" label="邮箱" width="180"></el-table-column>
      <el-table-column prop="mobile" label="电话" width="180"></el-table-column>
      <el-table-column label="用户状态">
        <template slot-scope="scope">
          <el-switch
            @change="state(scope.row.id,scope.row.mg_state)"
            v-model="scope.row.mg_state"
            active-color="#13ce66"
            inactive-color="#ff4949"
          ></el-switch>
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button
            @click="userscompile(scope.row.id)"
            size="mini"
            plain
            type="primary"
            icon="el-icon-edit"
          ></el-button>
          <el-button
            @click="usersdelete(scope.row.id)"
            size="mini"
            plain
            type="danger"
            icon="el-icon-delete"
          ></el-button>
          <el-button
            @click="usersallot(scope.row.id)"
            size="mini"
            plain
            type="primary"
            icon="el-icon-check"
          ></el-button>
        </template>
      </el-table-column>
    </el-table>

    <!-- 分页 -->
    <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        @next-click="nextPage"
        @prev-click="prevPage"
        :current-page="pagenum"
        :page-sizes="[1,5,10,15]"
        :page-size="pagesize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
      ></el-pagination>
    </div>
    <!-- 添加用户框 -->
    <el-dialog title="添加用户" :visible.sync="dialogFormVisible">
      <el-form :model="addObj">
        <el-form-item label="用户名" :label-width="formLabelWidth">
          <el-input v-model="addObj.username" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="密码" :label-width="formLabelWidth">
          <el-input v-model="addObj.password" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="邮箱" :label-width="formLabelWidth">
          <el-input v-model="addObj.email" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="电话" :label-width="formLabelWidth">
          <el-input v-model="addObj.mobile" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="role">确 定</el-button>
      </div>
    </el-dialog>
    <!-- 编辑用户模板 -->
    <el-dialog title="添加用户" :visible.sync="addusers">
      <el-form :model="addObj">
        <el-form-item label="用户名" :label-width="formLabelWidth">
          <el-input v-model="addObj.username" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="密码" :label-width="formLabelWidth">
          <el-input v-model="addObj.password" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="邮箱" :label-width="formLabelWidth">
          <el-input v-model="addObj.email" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="电话" :label-width="formLabelWidth">
          <el-input v-model="addObj.mobile" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="role">确 定</el-button>
      </div>
    </el-dialog>
  </el-card>
</template>

<script>
export default {
  data() {
    return {
      tableData: [],
      // 页码
      pagenum: 1,
      // 显示条数
      pagesize: 5,
      // 数据总条数
      total: 0,
      search: "",
      value2: true,
      gridData: [],
      dialogFormVisible: false,
      addObj: {
        name: "",
        region: "",
        date1: "",
        delivery: false,
        type: [],
        resource: "",
        desc: ""
      },
      formLabelWidth: "120px",
      // 编辑用户开关
      addusers:false
    };
  },
  methods: {
    // 获取数据
    async datalist(pagenum, pagesize) {
      console.log(pagenum);
      console.log(pagesize);
      var rse = await this.$http.get(
        `/users?query=${this.search}&pagenum=${pagenum}&pagesize=${pagesize}`
      );
      console.log(rse);
      var { data, meta } = rse.data;
      if (meta.status === 200) {
        // 用户数据赋值
        this.tableData = data.users;
        console.log(this.tableData);
        // 数据总条数赋值
        this.total = data.total;
      } else {
        this.$message.error(meta.msg);
      }
    },
    // 点击修改用户状态
    async state(id, type) {
      console.log(id);
      console.log(type);
      var res = await this.$http.request({
        url: `users/${id}/state/${type}`,
        method: "put"
      });
      var { meta } = res.data;
      if (meta.status === 200) {
        console.log(meta);
        this.$message({
          message: meta.msg,
          type: "success"
        });
      } else {
        this.$message.error(meta.msg);
      }
    },
    // 点击下一页
    nextPage(val) {
      this.datalist(val);
    },
    // 点击上一页
    prevPage(val) {
      this.datalist(val);
    },
    // 当前页发生改变时触发
    handleCurrentChange(val) {
      this.datalist(val);
    },
    // 每页条数改变触发
    handleSizeChange(val) {
      console.log(val);
      this.datalist(this.pagenum, val);
    },
    // 添加用户
    async role() {
      console.log(123);
      var res = await this.$http.request({
        url: "/users",
        method: "post",
        data: this.addObj
      });
      console.log(res);
      var { meta } = res.data;
      if (meta.status === 201) {
        this.$message({
          message: meta.msg,
          type: "success"
        });
        this.dialogFormVisible = false;
        this.addObj = {};
      } else {
        this.$message.error(meta.msg);
      }
    },
    // 编辑
    userscompile(id){
      this.addusers=true
      var res = this.$http.get(`/users/${id}`)
      console.log(res)
      var {meta,data} = res.data
    }
  },
  mounted() {
    this.datalist(this.pagenum, this.pagesize);
  }
};
</script>

<style>
.el-breadcrumb {
  margin-bottom: 20px;
}
.bg-purple-light {
  padding-left: 10px;
}
</style>
