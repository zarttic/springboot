<template>
<div style="line-height: 60px; display: flex" >
  <div style="flex: 1; ">
    <span :class="collapseBtnClass" style="cursor: pointer; font-size: 18px" @click="collapse" />
    <el-breadcrumb separator="/" style="display: inline-block; margin-left: 10px">
      <el-breadcrumb-item :to="'/'">首页</el-breadcrumb-item>
      <el-breadcrumb-item>{{ currentPathName }}</el-breadcrumb-item>
    </el-breadcrumb>
  </div>


  <el-dropdown style="width: 100px; cursor: pointer">
    <div style="display: inline-block">
      <img :src="user.avatarUrl" alt=""
           style="width: 30px; border-radius: 50%; position: relative; top: 10px; right: 5px">
      <span>{{ user.nickname }}</span><i class="el-icon-arrow-down" ></i>
      <el-dropdown-menu slot="dropdown" style="width: 100px; text-align: center">
        <el-dropdown-item style="font-size: 15px; padding: 10px 0">
          <router-link to="/person">个人信息</router-link>
        </el-dropdown-item>
        <el-dropdown-item style="font-size: 14px; padding: 5px 0">
          <span style="text-decoration: none" @click="logout">退出</span>
        </el-dropdown-item>
      </el-dropdown-menu>
    </div>

  </el-dropdown>
</div>

</template>

<script>
export default {
  name: "Header",
  props: {
    collapseBtnClass: String,
  },
  methods: {
    collapse() {
      this.$emit("asideCollapse")
    },
    logout(){
      this.$router.push("/login")
      localStorage.removeItem("user")
      this.$message.success("退出成功")
    }
  },
  watch: { //监听路由变化
    '$route':function (){
      this.currentPathName = localStorage.getItem("currentPathName")
    }
    },
  data(){
    return{
      currentPathName: '',
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {}
    }
  }
  }
</script>

<style scoped>

</style>