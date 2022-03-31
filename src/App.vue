<template>
    <div class="ms-3 me-3">
    <div
      v-for="article in articles"
      :key="article.id"
      class="py-3 mx-12"
    >
      <Article
        :article="article"
        @addLike="addLike"
        @subtractLike="subtractLike"
        @deleteArticle="deleteArticle"
      />
    </div>
    <div class="alert-info p-2 mt-2 mb-5 text-center">Number of articles: {{ articles.length }}</div>
    <Form @addArticle="addArticle" />
    <button
      class="btn btn-secondary mb-3 mt-3 d-grid gap-2 col-2 mx-auto"
      @click="importArticles"
    >
      Import articles
    </button>
  </div>
</template>

<script>
import Article from '@/components/Article'
import Form from '@/components/Form'
import { ARTICLES } from '@/constants/articles'

export default {
  name: 'App',
  components: {
    Article,
    Form,
  },
  data: () => {
    return {
      articles: ARTICLES,
    }
  },
  methods: {
    addLike(id) {
      const articleIndex = this.articles.findIndex((article) => article.id === id)
      this.articles[articleIndex].likeCount += 10
    },
    subtractLike(id) {
      const articleIndex = this.articles.findIndex((article) => article.id === id)
      this.articles[articleIndex].likeCount -= 20
    },
    addArticle({ title, body }) {
      this.articles.push({
        id: this.articles.at(-1)?.id + 1 || 0,
        title,
        body,
        likeCount: 0,
      })
    },
    importArticles() {
      fetch('https://jsonplaceholder.typicode.com/posts?userId=1')
        .then((response) => response.json())
        .then((data) => {
          for (const article of data) {
            delete article.userId
            article.likeCount = 0
            article.id = this.articles.at(-1)?.id + 1 || 0
            this.articles.push(article)
          }
        })
    },
    deleteArticle(id) {
      const articleIndex = this.articles.findIndex((article) => article.id === id)
      this.articles.splice(articleIndex, 1)
    },
  },
}
</script>
