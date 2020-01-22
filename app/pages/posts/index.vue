<template>
  <section class="container posts-page">
    <el-card>
      <!-- slot はテンプレートタグ内の文字列を slot タグへと入れ替える -->
      <div slot="header" class="clearfix">
        <span>新着投稿</span>
      </div>
      <el-table :data="showPosts" class="table" style="width: 100%;">
        <el-table-column prop="title" label="タイトル" />
        <el-table-column prop="user.id" label="投稿者" width="180" />
        <el-table-column prop="created_at" label="投稿日時" width="240" />
      </el-table>
    </el-card>
  </section>
</template>

<script>
import { mapGetters } from 'vuex'
import moment from '~/plugins/moment'

export default {
  computed: {
    showPosts () {
      return this.posts.map((post) => {
        post.created_at = moment(post.created_at).format('YYYY/MM/DD HH:mm:ss')
        return post
      })
    },
    ...mapGetters('posts', ['posts'])
  },
  async asyncData ({ store }) {
    await store.dispatch('posts/fetchPosts')
  },
  methods: {
    handleClick (post) {
      this.$router.push(`/posts/${post.id}`)
    }
  }
}
</script>

<style>
.posts-page .el-table__row {
  cursor: pointer;
}
</style>
