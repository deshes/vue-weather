<template>
  <el-container>
    <el-aside width="260px" style="background-color: rgb(238, 241, 246)">
      <img src alt style="display:block;background-color:#409EFF;width:100%;height:60px;" />
      <el-menu>
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-message"></i>天气预报
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
          </el-menu-item-group>
          <el-menu-item-group title="分组2"></el-menu-item-group>
        </el-submenu>
        <el-submenu index="2">
          <template slot="title">
            <i class="el-icon-menu"></i>导航二
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="2-1">选项1</el-menu-item>
            <el-menu-item index="2-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="2-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="2-4">
            <template slot="title">选项4</template>
            <el-menu-item index="2-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-submenu index="3">
          <template slot="title">
            <i class="el-icon-setting"></i>导航三
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="3-1">选项1</el-menu-item>
            <el-menu-item index="3-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="3-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="3-4">
            <template slot="title">选项4</template>
            <el-menu-item index="3-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
      </el-menu>
    </el-aside>

    <el-container>
      <el-header style="text-align: right; font-size: 12px">
        <el-dropdown>
          <i class="el-icon-setting" style="margin-right: 15px"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>查看</el-dropdown-item>
            <el-dropdown-item>新增</el-dropdown-item>
            <el-dropdown-item>删除</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <span>admin</span>
      </el-header>

      <el-main>
        <el-table :data="tableData">
          <el-table-column prop="week" label="日期" width="140"></el-table-column>
          <el-table-column prop="wea" label="天气" width="120"></el-table-column>
          <el-table-column prop="air" label="空气指数" width="120"></el-table-column>
          <el-table-column prop="air_level" label="空气等级" width="120"></el-table-column>
          <el-table-column prop="win_speed" label="风速"></el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </el-container>
</template>
 
<style>
.el-header {
  background-color: #409eff;
  color: #000;
  line-height: 60px;
}

.el-aside {
  color: #333;
}
</style>

<script>
export default {
  data() {
    return {
      tableData: []
    };
  },
  methods: {
    getData(cityCode) {
      if (!cityCode) {
        this.axios
          .get(`https://www.tianqiapi.com/api/`)
          .then((response) =>{
            console.log(response);
            this.tableData = response.data.data;
          });
      } else {
        this.axios
          .get(`https://www.tianqiapi.com/api/?version=v1&cityid=${cityCode}`)
          .then( (response) =>{
            // console.log(response);
            this.tableData = response.data;
          });
      }
    }
  },
  mounted() {
    // 调用请求数据的方法
    this.getData();
  }
};
</script>