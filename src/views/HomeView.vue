<template>
  <div>
    <el-container style="height: 100%; border: 1px solid #eee">
      <el-aside width="'sideWidth'+px" style="background-color: rgb(238, 241, 246);height: 100%">
        <el-menu :default-openeds="['1', '3']" style="height: 100%;overflow-x: hidden" background-color="rgb(48,65,86)"
                 text-color="white" active-text-color="#ffd14c" :collapse="isCollapse" :collapse-transition="false">
            <div style="height: 60px; text-align: center; line-height: 60px">
                <img src="../assets/logo.png" style="width: 25px; margin-right: 5px; top:5px;position: relative">
                <b style="color: white; font-weight: bold; font-size: 20px" v-show="logoTextShow">后台管理系统</b>
            </div>

            <el-submenu index="1">
            <template slot="title">
                <i class="el-icon-message"></i>
                <span slot="title">导航一</span>
            </template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="1-1">选项1</el-menu-item>
              <el-menu-item index="1-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="1-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
              <template slot="title">选项4</template>
              <el-menu-item index="1-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
                <i class="el-icon-menu"></i>
                <span slot="title">导航二</span>
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
                <i class="el-icon-setting"></i>
                <span slot="title">导航三</span>
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
<!--        头部-->
        <el-header style=" font-size: 12px; line-height: 60px; display: flex">
          <div style="flex: 1; font-size: 18px">
            <span :class="collapseBtnClass" style="cursor: pointer" @click="collapse"></span>
          </div>

          <el-dropdown style="width: 200px;text-align: right">
            <span>王小虎</span><i class="el-icon-arrow-down" style="margin-left: 5px; font-size: 16px"></i>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>个人信息</el-dropdown-item>
              <el-dropdown-item>退出登录</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>

        </el-header>

        <el-main style="border-top: 1px solid #efefef">

            <div>
                <el-breadcrumb separator-class="el-icon-arrow-right">
                    <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
                    <el-breadcrumb-item>用户管理</el-breadcrumb-item>
                </el-breadcrumb>
            </div>
            <div style="height: 70px; line-height: 70px">
                <el-input v-model="input" placeholder="请输入用户名" style="width: 200px; margin-right: 10px" suffix-icon="el-icon-search"></el-input>
                <el-input v-model="input" placeholder="请输入邮箱" style="width: 200px; margin-right: 10px" suffix-icon="el-icon-message"></el-input>
                <el-input v-model="input" placeholder="请输入地址" style="width: 200px; margin-right: 10px" suffix-icon="el-icon-location"></el-input>

                <el-button  type="primary">搜索</el-button>
            </div>

            <div>
                <el-button type="primary"  icon="el-icon-circle-plus-outline">新增</el-button>
                <el-button type="danger"  icon="el-icon-remove-outline">批量删除</el-button>
                <el-button type="primary"  icon="el-icon-upload2">导入</el-button>
                <el-button type="primary"  icon="el-icon-download">导出</el-button>
            </div>

          <el-table :data="tableData" :header-cell-style="{background:'#F3F4F7'}">
            <el-table-column prop="date" label="日期" width="140">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column prop="address" label="地址">
            </el-table-column>
              <el-table-column label="操作">
                  <template>
                      <el-button type="success"  icon="el-icon-edit">编辑</el-button>
                      <el-button type="danger" icon="el-icon-delete">删除</el-button>
                  </template>
              </el-table-column>
          </el-table>
<!--            分页-->
            <div style="padding: 10px 0">
                <el-pagination
                        @size-change="handleSizeChange"
                        @current-change="handleCurrentChange"
                        :current-page="currentPage4"
                        :page-sizes="[100, 200, 300, 400]"
                        :page-size="100"
                        layout="total, sizes, prev, pager, next, jumper"
                        :total="400">
                </el-pagination>
            </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  data() {
    const item = {
      date: '2016-05-02',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1518 弄'
    };
    return {
      tableData: Array(10).fill(item),
      isCollapse:false,
      collapseBtnClass: 'el-icon-s-fold',
        sideWidth:200,
        logoTextShow: true
    }
  },
    methods:{
        //点击收缩按钮
        collapse(){
            this.isCollapse = !this.isCollapse
            if(this.isCollapse){
                this.sideWidth = 64
                this.collapseBtnClass = 'el-icon-s-unfold'
                this.logoTextShow = false
            }else{
                this.collapseBtnClass = 'el-icon-s-fold'
                this.sideWidth = 200
                this.logoTextShow = true
            }
        }
    }
}
</script>

<style>
  .el-header {
    /*background-color: #B3C0D1;*/
    /*color: #333;*/
    line-height: 60px;
  }

  .el-aside {
    color: #333;
  }
</style>
