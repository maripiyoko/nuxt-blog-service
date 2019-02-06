<template>
  <section class="container posts-page">
    <div style="flex: 1">
      <el-card v-if="post">
        <div slot="header" class="clearfix">
          <h2>
            {{post.title}}
          </h2>
          <small>by {{post.user.id}}</small>
        </div>
        <p>
          {{post.body}}
        </p>
      </el-card>
    </div>
  </section>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  async asyncData({ store, route }) {
    if (store.getters['posts/posts'].find(p => p.id === route.params.id)) {
      return
    }
    await store.dispatch('posts/fetchPosts')
  },
  computed: {
    post() {
      return this.posts.find(p => p.id === this.$route.params.id)
    },
    ...mapGetters('posts', ['posts'])
  }
}
</script>
