# PLUGINS

**This directory is not required, you can delete it if you don't want to use it.**

This directory contains Javascript plugins that you want to run before mounting the root Vue.js application.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/guide/plugins).

pluginsディレクトリは、NPMパッケージやプラグインなどをグローバルに登録し、再利用性を高めるために用いられる。

具体的には、Firebase, SDK, Day.jsなど必ずアプリ全体で使うことが明確なライブラリなど。

pluginsディレクトリに、該当するプラグインを登録したのちに
nuxt.config.jsディレクトリに

module.exports = {
  // ...
  plugins: ["~/plugins/..."]
  // ...
}

を追記する。
