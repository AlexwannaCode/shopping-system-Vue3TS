<template>
  <div class="home">
    <el-container>
      <el-header>
        <el-row :gutter="20">
          <el-col :span="4">
            <img class="logo" src="../assets/logo.png" alt="logo">
          </el-col>
          <el-col :span="16">
            <h2>后台管理系统</h2>
          </el-col>
          <el-col :span="4" class="col-btn">
            <el-button link type="primary" @click="logout">退出登录</el-button>
          </el-col>
        </el-row>
      </el-header>

      <el-container>
        <el-aside width="200px">
          <el-menu active-text-color="#ffd04b" background-color="#545c64" class="el-menu-vertical-demo"
            default-active="active" text-color="#fff" router>

            <el-menu-item v-for="(item) in showList" :index="item.path" :key="item.path">
              <span>{{ item.meta.title }}</span>
            </el-menu-item>
          </el-menu>
        </el-aside>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script lang="ts">
// import { defineComponent } from "vue";
import { useRouter, useRoute } from "vue-router";


export default {
  name: "HomeView",
  setup() {
    const router = useRouter()
    const route = useRoute()
    const showList = router.getRoutes().filter(v => v.meta.isShow)

    const logout = () => {
      localStorage.removeItem('token')
      router.push("/login")
    }
    return {
      showList, active: route.path, logout
    }
  }
};
</script>

<style lang="scss">
.el-header {
  height: 80px;
  background-color: #666;

  .logo {
    height: 80px;
  }

  h2,
  .quit-login {
    text-align: center;
    color: white;
    height: 80px;
    line-height: 80px;
  }
}

.col-btn {
  height: 80px;
  line-height: 80px;
}

.el-aside {
  .el-menu {
    height: calc(100vh - 80px);
  }
}
</style>
