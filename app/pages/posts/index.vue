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
export default {
  computed: {
    showPosts () {
      return [
        {
          id: '001',
          title: 'How to development Nuxt.js Application',
          body: 'Hello World1',
          created_at: '2020/01/22 13:00',
          user: {
            id: 'torish14'
          }
        },
        {
          id: '002',
          title: 'Development Nuxt.js Application to Heroku',
          body: 'Hello World2',
          created_at: '2020/01/22 13:30',
          user: {
            id: 'torish14'
          }
        }
      ]
    }
  }
}
</script>

<style>
.posts-page .el-table__row {
  cursor: pointer;
}
</style>
