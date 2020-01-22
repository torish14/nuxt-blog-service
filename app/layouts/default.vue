<template>
  <div>
    <TheHeader />
    <div class="wrapper">
      <!-- コンポーネントが含まれるようにレイアウトを変更する場合は、必ず <nuxt /> コンポーネントを追加する -->
      <nuxt class="container" />
    </div>
  </div>
</template>

<script>
import TheHeader from '~/components/TheHeader.vue'

export default {
  components: {
    TheHeader
  }
}
</script>
