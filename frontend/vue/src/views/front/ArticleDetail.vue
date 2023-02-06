<template>
  <div style="color: #666">
    <div style="margin: 20px 0; ">
      <div class="pd-10" style="font-size: 20px; color: #3F5EFB; cursor: pointer">{{ article.name }}</div>
      <div style="font-size: 14px; margin-top: 10px">
        <i class="el-icon-user-solid"></i> <span>{{ article.user }}</span>
        <i class="el-icon-time" style="margin-left: 10px"></i> <span>{{ article.time }}</span>
      </div>
    </div>

   <div style="margin: 20px 0">
     <mavon-editor
         class="md"
         :value="article.content"
         :subfield="false"
         :defaultOpen="'preview'"
         :toolbarsFlag="false"
         :editable="false"
         :scrollStyle="true"
         :ishljs="true"
     />
   </div>

    <div style="margin: 30px 0">
      <div style="margin: 10px 0">
        <div style="border-bottom: 1px solid orangered; padding: 10px 0; font-size: 20px">评论</div>
        <div style="padding: 10px 0">
          <el-input size="small" type="textarea" v-model="commentForm.content"></el-input>
        </div>
        <div class="pd-10" style="text-align: right">
          <el-button type="primary" size="small" @click="save">comment</el-button>
        </div>
      </div>


      <div>
        <div v-for="item in comments" :key="item.id" style="border-bottom: 1px solid #ccc; padding: 10px 0; ">
          <div style="display: flex">
            <div style="width: 100px; text-align: center">
              <el-image :src="item.avatarUrl" style="width: 50px; height: 50px; border-radius: 50%"></el-image>
            </div> 
            <div style="flex: 1; font-size: 14px; padding: 5px 0; line-height: 25px">
              <b>{{ item.nickname }}：</b>
              <span>{{ item.content }}</span>

              <div style="display: flex; line-height: 20px; margin-top: 5px">
                <div style="width: 200px;">
                  <i class="el-icon-time"></i><span style="margin-left: 5px">{{ item.time }}</span>
                </div>
                <div style="text-align: right; flex: 1">
                  <el-button style="margin-left: 5px" type="text" @click="handleReply(item.id)">reply</el-button>
                  <el-button type="text" style="color: red" @click="del(item.id)" v-if="user.id === item.userId">delete</el-button>
                </div>
              </div>
            </div>   
          </div>

          <div v-if="item.children.length"  style="padding-left: 200px;">
            <div v-for="subItem in item.children" :key="subItem.id"  style="background-color: #f0f0f0; padding: 5px 20px">

              <div style="font-size: 14px; padding: 5px 0; line-height: 25px">
                <div>
                  <b style="color: #3a8ee6" v-if="subItem.pnickname">@{{ subItem.pnickname }}</b>
                </div>
                <div style="padding-left: 5px">
                  <b>{{ subItem.nickname }}：</b>
                  <span>{{ subItem.content }}</span>
                </div>

                <div style="display: flex; line-height: 20px; margin-top: 5px; padding-left: 5px">
                  <div style="width: 200px;">
                    <i class="el-icon-time"></i><span style="margin-left: 5px">{{ subItem.time }}</span>
                  </div>
                  <div style="text-align: right; flex: 1">
                    <el-button style="margin-left: 5px" type="text" @click="handleReply(subItem.id)">reply</el-button>
                    <el-button type="text" style="color: red" @click="del(subItem.id)" v-if="user.id === subItem.userId">delete</el-button>
                  </div>
                </div>
              </div>   
            </div>

          </div>


        </div>
      </div>
    </div>


    <el-dialog title="reply" :visible.sync="dialogFormVisible" width="50%" >
      <el-form label-width="80px" size="small">
        <el-form-item label="reply content">
          <el-input type="textarea" v-model="commentForm.contentReply" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false" size="small">cancel</el-button>
        <el-button type="primary" @click="save"  size="small">confirm</el-button>
      </div>
    </el-dialog>

  </div>
</template>

<script>

export default {
  name: "Article",
  data() {
    return {
      article: {},
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {},
      comments: [],
      commentForm: {},
      id: this.$route.query.id,
      dialogFormVisible: false
    }
  },
  created() {
    this.load()
    this.loadComment()
  },
  methods: {
    load() {
      this.request.get("/article/" + this.id).then(res => {
        this.article = res.data
      })
    },
    loadComment() {
      this.request.get("/comment/tree/" + this.id).then(res => {
        this.comments = res.data
      })
    },
    save() {
      if (!this.user.id) {
        this.$message.warning("please log in first")
        return
      }
      this.commentForm.articleId = this.id
      if (this.commentForm.contentReply) {
        this.commentForm.content = this.commentForm.contentReply
      }
      this.request.post("/comment", this.commentForm).then(res => {
        if (res.code === '200') {
          this.$message.success("successfully reply!")
          this.commentForm = {}  
          this.loadComment()
          this.dialogFormVisible = false
        } else {
          this.$message.error(res.msg)
        }
      })
    },
    del(id) {
      this.request.delete("/comment/" + id).then(res => {
        if (res.code === '200') {
          this.$message.success("deleted")
          this.loadComment()
        } else {
          this.$message.error("failed to delete")
        }
      })
    },
    handleReply(pid) {
      this.commentForm = { pid: pid }
      this.dialogFormVisible = true
    }
  }
}
</script>

<style scoped>

</style>
