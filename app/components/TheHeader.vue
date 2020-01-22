<template>
  <el-menu :router="true" mode="horizontal">
    <el-menu-item index="1" style="pointer-events: none;">
      Nuxt Diary App
    </el-menu-item>
    <el-menu-item :route="{ path: '/posts/' }" index="2">
      投稿一覧
    </el-menu-item>

    <no-ssr>
      <!-- 自分がログインしているか確認するために、ログイン中はユーザーの情報を表示できるようにする -->
      <el-menu-item :route="{ path: `/users/${user.id}` }" v-if="user" index="4" style="float: right;">
        <span>{{ user.id }}</span>
      </el-menu-item>
      <el-menu-item :route="{ path: '/' }" v-else index="4" style="float: right;">
        <span>ログイン</span>
      </el-menu-item>
    </no-ssr>
    <el-menu-item :route="{ path: '/posts/new' }" index="5" style="float: right;">
      新規登録
    </el-menu-item>
  </el-menu>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['user'])
  }
}
</script>
