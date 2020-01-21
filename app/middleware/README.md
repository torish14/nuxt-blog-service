# MIDDLEWARE

**This directory is not required, you can delete it if you don't want to use it.**

This directory contains your application middleware.
Middleware let you define custom functions that can be run before rendering either a page or a group of pages.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/guide/routing#middleware).

middlewareディレクトリは、Nuxt.jsの中でも最も強力である。

ミドルウェアは、グローバルを含めた任意のルーティングへのアクセス時に読み込まれ、SSR処理の前に多くの処理を行うことが可能。

例えば、ユーザーエージェントに合わせたに合わせたリダイレクトや認証許可の必要なページの構築が、簡単となる。
