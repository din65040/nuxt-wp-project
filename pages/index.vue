<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxt-wp-project
      </h1>
      <h2 class="subtitle">
        My outstanding Nuxt.js x WordPress project
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
      <article v-for="post in posts" :key="post.id">
        <n-link :to="{ path: '/posts/' + post.id }">
          <h2>{{ post.title.rendered }}</h2>
          <div v-html="post.excerpt.rendered"></div>
        </n-link>
      </article>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  data () {
    return {
      posts: []
    }
  },
  components: {
    Logo
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get('/posts')
    return { posts: data }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
