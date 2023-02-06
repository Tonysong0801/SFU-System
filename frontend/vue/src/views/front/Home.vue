<template>
  <div>
    <div style="margin: 10px 0">
      <el-carousel height="450px" :interval="10000">
        <el-carousel-item v-for="item in imgs" :key="item">
          <img :src="item" alt="" style="width: 100%">
        </el-carousel-item>
      </el-carousel>
    </div>

    <div style="margin: 10px 0">
      <el-row :gutter="10">
        <el-col :span="6" v-for="item in files" :key="item.id" style="margin-bottom: 10px">

          <div style="border: 1px solid #ccc; padding-bottom: 10px">
            <img :src="item.url" alt="" style="width: 100%">
            <div style="color: #666; padding: 10px">{{ item.name }}</div>
            <div style="padding: 10px"><el-button type="primary">purchase</el-button></div>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
export default {
  name: "FrontHome",
  data() {
    return {
      imgs: [
          'https://m.media-amazon.com/images/I/61bgF83DPjL._SX3000_.jpg',
          'https://m.media-amazon.com/images/I/61fgwOtr9jL._SX3000_.jpg',
          'https://m.media-amazon.com/images/I/71Bzjp8cD4L._SX3000_.jpg'
      ],
      files: []
    }
  },
  created() {
    this.request.get("/echarts/file/front/all").then(res => {
      console.log(res.data)
      this.files = res.data.filter(v => v.type === 'png' || v.type === 'jpg' || v.type === 'webp')
    })
  },
  methods: {

  }
}
</script>

<style>

</style>
