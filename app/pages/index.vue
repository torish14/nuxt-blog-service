<template>
  <section class="container">
    <el-card style="flex: 1;">
      <div class="clearfix" sloy="header">
        <span>ログイン</span>
      </div>
      <form>
        <div class="form-content">
          <span>ユーザー ID</span>
          <el-input v-model="formData.id" placeholder="" />
        </div>
        <div class="form-content">
          <el-checkbox v-model="isCreateMode">
            アカウントを作成する
          </el-checkbox>
        </div>
        <div class="text-right">
          <el-button @click="handleClickSubmit" type="primary">
            {{ buttonText }}
          </el-button>
        </div>
      </form>
    </el-card>
  </section>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
// クッキーの追記
import Cookies from 'universal-cookie'

export default {
  computed: {
    buttonText () {
      return this.isCreateMode ? '新規登録' : 'ログイン'
    },
    ...mapGetters(['user'])
  },
  // asyncData は、コンポーネントがロードされる前に毎回呼び出される
  asyncData ({ redirect, store }) {
    if (store.getters.user) {
      redirect('/posts/')
    }
    return {
      isCreateMode: false,
      formData: {
        id: ''
      }
    }
  },
  methods: {
    async handleClickSubmit () {
      //! クッキーインスタンスの生成
      const cookies = new Cookies()
      if (this.isCreateMode) {
        try {
          await this.resiter({ ...this.formData })
          this.$notify({
            type: 'success',
            title: 'アカウント作成完了',
            message: `${this.formData.id} として登録しました`,
            position: 'bottom-right',
            duration: 1100
          })
          //! JSON.stringifyメソッドは、JSON文字列に変換する
          cookies.set('user', JSON.stringify(this.user))
          this.$router.push('/posts/')
        } catch (e) {
          this.$notify.error({
            title: 'アカウント作成失敗',
            message: 'すでに登録されているか、不正なユーザー ID です',
            position: 'bottom-right',
            duration: 1100
          })
        }
      } else {
        try {
          await this.login({ ...this.formData })
          this.$notify({
            type: 'success',
            title: 'ログイン成功',
            message: `${this.formData.id} としてログインしました`,
            positon: 'bottom-right',
            duration: 1100
          })
          //! JSON.stringifyメソッドは、JSON文字列に変換する
          cookies.set('user', JSON.stringify(this.user))
          this.$router.push('/posts/')
        } catch (e) {
          this.$notify.error({
            title: 'ログイン失敗',
            mesage: '不正なユーザー iD です',
            position: 'bottom-right',
            duration: 1100
          })
        }
      }
    },
    ...mapActions(['login', 'register'])
  }
}
</script>

<style>
.form-content {
  margin: 16px 0;
}
</style>
