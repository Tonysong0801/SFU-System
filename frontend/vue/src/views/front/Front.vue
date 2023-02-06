<template>
  <div>
<!--    头部-->
    <div style="display: flex; height: 60px; line-height: 60px; border-bottom: 1px solid #eee">
      <div style="width: 300px; display: flex; padding-left: 30px">
        <div style="width: 60px">
          <img src="../../assets/sfu.png" alt="" style="width: 50px; position: relative; top: 5px; right: 0">
        </div>
        <div style="flex: 1">Welcome to Online Market</div>
      </div>
      <div style="flex: 1">



        <el-menu :default-active="'1'" class="el-menu-demo" mode="horizontal" router>
          <el-menu-item index="/front/home">Main Page</el-menu-item>
          <el-menu-item index="/front/video">Videos</el-menu-item>
          <el-menu-item index="/front/article">Article</el-menu-item>
          <el-submenu index="2">
            <template slot="title">My workbench</template>
            <el-menu-item index="/front/item1">option1</el-menu-item>
            <el-menu-item index="2-2">option2</el-menu-item>
            <el-menu-item index="2-3">option3</el-menu-item>
            <el-submenu index="2-4">
              <template slot="title">option4</template>
              <el-menu-item index="2-4-1">1</el-menu-item>
              <el-menu-item index="2-4-2">2</el-menu-item>
              <el-menu-item index="2-4-3">3</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-menu-item index="3" disabled>messages</el-menu-item>
          <el-menu-item index="4"><a href="https://www.ubereats.com/ca" target="_blank">Delivery oders</a></el-menu-item>
        </el-menu>
      </div>
      <div style="width: 200px">
        <div v-if="!user.username" style="text-align: right; padding-right: 30px">
          <el-button @click="$router.push('/login')">Log in</el-button>
          <el-button @click="$router.push('/register')">Register</el-button>
        </div>
        <div v-else>
          <el-dropdown style="width: 150px; cursor: pointer; text-align: right">
            <div style="display: inline-block">
              <img :src="user.avatarUrl" alt=""
                   style="width: 30px; border-radius: 50%; position: relative; top: 10px; right: 5px">
              <span>{{ user.nickname }}</span><i class="el-icon-arrow-down" style="margin-left: 5px"></i>
            </div>
            <el-dropdown-menu slot="dropdown" style="width: 100px; text-align: center">
              <el-dropdown-item style="font-size: 14px; padding: 5px 0">
                <router-link to="/front/password">change password</router-link>
              </el-dropdown-item>
              <el-dropdown-item style="font-size: 14px; padding: 5px 0">
                <router-link to="/front/person">personal information</router-link>
              </el-dropdown-item>
              <el-dropdown-item style="font-size: 14px; padding: 5px 0">
                <span style="text-decoration: none" @click="logout">Log out</span>
              </el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
      </div>
    </div>

    <div style="width: 1000px; margin: 0 auto">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: "Front",
  data() {
    return {
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {}
    }
  },
  created() {

  },
  methods: {
    logout() {
      this.$store.commit("logout")
      this.$message.success("Successfully log out!")
    }
  }
}
</script>

<style>
.item{
  display: inline-block;
  width: 100px;

  text-align: center;
  cursor: pointer
}
.item a {
  color: 	#1E90FF;
}
.item:hover{
  background-color: 	LightPink;
}
</style>
