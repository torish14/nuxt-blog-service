<template>
  <section class="container posts-page">
    <el-card style="flex: 1;">
      <!-- slot はテンプレートタグ内の文字列を slot タグへと入れ替える -->
      <div slot="header" class="clearfix">
        <el-input v-model="formData.title" placeholder="タイトルを入力" />
      </div>
      <div>
        <el-input v-model="formData.body" placeholder="本文を入力・・・" type="textarea" rows="15" />
      </div>
      <div class="text-right" style="margin-top: 16px;">
        <el-button @click="publish" type="primary" round>
          <span class="el-icon-upload2" />
          <span>Publish</span>
        </el-button>
      </div>
    </el-card>
  </section>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'

export default {
  computed: {
    //! ...obj はスプレッド記法といい、式を複数の要素に展開して配列の値に渡す
    ...mapGetters(['user'])
  },
  asyncData ({ redirect, store }) {
    if (!store.getters.user) {
      redirect('/')
    }
    return {
      formData: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    async publish () {
      const payload = {
        user: this.user,
        ...this.formData
      }
      await this.publishPost({ payload })
      this.$router.push('/posts')
    },
    ...mapActions('users', ['updateUser']),
    ...mapGetters('posts', ['publishPost'])
  }
}
</script>

<style>
.posts-page .el-table__row {
  cursor: pointer;
}
</style>
