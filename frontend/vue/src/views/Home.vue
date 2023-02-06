<template>
  <div style="color: #666;font-size: 14px;">
    <div style="padding-bottom: 20px">
      <b>Welcome！{{ user.nickname }}</b>
    </div>
    <el-card>
      A fantastic system
      <el-divider />
      booted by Springboot+Vue<b>99</b>dollar<br><br>
      made by Tony Song from SFU<b>9.9</b>department of Computer Science<br><br>
      <a style="color: #1E90FF" href="https://www.sfu.ca/dashboard/students.html" target="_blank">SFU students website</a>
      <a style="color: red; font-size: 20px" href="https://www.sfu.ca/" target="_blank">SFU Main page</a><br><br>
    </el-card>
    <div style="height: 1px; background: #ddd; margin: 20px 0"/>

    <el-row :gutter="30">
      <el-col :span="12">
        <div style="padding: 20px 0; font-size: 20px">Information Management System</div>
        <div>
          Authur: Tony Song, All rights reserved
        </div>
        <div class="m-10"><el-button type="danger"><i class="el-icon-coin"></i> open source</el-button></div>
        <div class="m-10"><el-button type="primary"><i class="el-icon-s-custom"></i> what is milly capable of</el-button>
          <el-button type="primary">715739443</el-button></div>
        <div class="m-10">
          <el-button type="primary"><i class="el-icon-link"></i> <a style="color: #fff" href="https://github.com/">Github site</a></el-button>
          <el-button type="primary"><i class="el-icon-link"></i> <a style="color: #fff" href="https://www.youtube.com/watch?v=3I9nGdPB_Sg&t=122s">youtube site</a></el-button>
        </div>
      </el-col>
      <el-col :span="12">
        <div style="padding: 20px 0; font-size: 20px">skill sets</div>
        <el-row>
          <el-col :span="12" style="line-height: 30px">
            <div><b>backend</b></div>
            <div>SpringBoot2</div>
            <div>Hutool</div>
            <div>Poi</div>
            <div>Lombok</div>
            <div>Mybatis/Mybatis-plus</div>
          </el-col>
          <el-col :span="12" style="line-height: 30px">
            <b>frontend</b>
            <div>Vue2</div>
            <div>Vue-Router</div>
            <div>VueX</div>
            <div>ElementUI</div>
            <div>Axios</div>
          </el-col>
        </el-row>
      </el-col>
    </el-row>

  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {}
    }
  }
}
</script>
