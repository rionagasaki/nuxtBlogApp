<template>
  <section>
      <el-card>
         <div slot="header" class="clearfix">
             <span>新着投稿</span>
         </div> 
      <el-table 
      :data="showPosts" 
      style="width: 100%;" 
      @row-click="handleClick"
      class="table">
          <el-table-column 
      prop="title" 
      label="タイトル">
          </el-table-column>
          <el-table-column 
      prop="user.id"
      label="投稿者"
      width="180"
      >
          </el-table-column>
          <el-table-column 
      prop="createdAt"
      label="投稿日時"
      width="240"
      >
          </el-table-column>

      </el-table>
      </el-card>
  </section>
</template>

<script>
import { mapGetters } from 'vuex'
import moment from '~/plugins/moment'


export default {
    async asyncData({store}){
      await store.dispatch('posts/fetchPosts')
    },
    computed:{
        showPosts(){
            return this.posts.map(post => {
                post.createdAt = moment(post.createdAt).format('YYYY/MM/DD HH:mm:ss')
                return post
            })
        },
        ...mapGetters('posts', ['posts']),
       
    },
    methods:{
        handleClick(post) {
            this.$router.push(`/posts/${post.id}`)
        }
    }

}
</script>

<style>
  
</style>