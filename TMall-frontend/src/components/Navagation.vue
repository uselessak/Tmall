<!--
 * 前台页面-导航栏
 *
 * @Author: ShanZhu
 * @Date: 2023-11-11
-->
<template>
  <div class="navagation">
    <el-row>

      <el-col :span="3">
        <div style="font-size: 20px; font-weight: bold; text-align: center">
          <a href="/"> <img src="../resource/logo.png" style="width: 40px;position: relative; top: 13px;right: 6px">网上购物商城</a>
        </div>
      </el-col>

      <el-col :span="17">
        <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal"router>

          <el-menu-item index="/" class="menu-item">商城首页</el-menu-item>
          <el-menu-item index="/goodList" class="menu-item">商品分类</el-menu-item>
          <el-menu-item index="/cart" class="menu-item">我的购物车</el-menu-item>
          <el-menu-item index="/orderlist" class="menu-item">我的订单</el-menu-item>
          <el-menu-item index="/manage" class="menu-item"v-if="role === 'admin'">后台管理</el-menu-item>

        </el-menu>
      </el-col>

      <el-col :span="4">

        <!--右上角个人信息-->
        <el-dropdown style="cursor: pointer; float: right; margin-right: 60px">
          <span class="el-dropdown-link">
            <div style="display: inline-block">
              <img
                v-if="user.avatarUrl != null"
                :src="baseApi + user.avatarUrl"
                class="avatar"
              />
              {{ user.nickname }}
              <i
                class="el-icon-arrow-down el-icon--right"
                style="margin-right: 5px"
              ></i>
            </div>
          </span>
          <!--跟人信息下拉菜单-->
          <el-dropdown-menu slot="dropdown" style="text-align: center">
            <el-dropdown-item>

              <!--传给前端，登录后跳转页面的path为 "/"-->
              <div @click="$router.push({ path: '/login', query: { to: '/' } })"v-show="!loginStatus">
                登录
              </div>
            </el-dropdown-item>

            <el-dropdown-item v-show="loginStatus">
              <div @click="$router.push('/person')">个人信息</div>
            </el-dropdown-item>

            <el-dropdown-item v-show="loginStatus">
              <div @click="logout">退出</div>
            </el-dropdown-item>

          </el-dropdown-menu>

        </el-dropdown>

      </el-col>
    </el-row>
  </div>
</template>


<script>
export default {
  name: "Navagation",
  props: {
    user: Object,
    loginStatus: Boolean,
    role: String,
  },
  //初始化数据
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",
      baseApi: this.$store.state.baseApi,
    };
  },
  methods: {
    //退出账号
    logout() {
      localStorage.removeItem("user");
      this.$router.go(0);
      this.$message.success("退出成功");
    },
  },
};
</script>
<style>
a {
  text-decoration: none;
}
.navagation {
  width: 100%;
  height: 60px;
  line-height: 60px;
  background-color: #ffffff;
  overflow: hidden;
}
.avatar {
  width: 30px;
  border-radius: 50%;
  position: relative;
  top: 10px;
  right: 5px;
}
.menu-item {
  padding-left: 50px;
  padding-right: 50px;
}
</style>
