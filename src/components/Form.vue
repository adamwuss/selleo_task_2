<template>
  <div class="col-md-10 mx-auto col-lg-5">
    <form class="p-4 p-md-5 border rounded-3 bg-light">
      <div class="form-floating mb-3">
        <input
          type="text"
          class="form-control"
          :class="validationTitle && 'validation'"
          v-model="title"
        />
        <label>
          Title
        </label>
      </div>
      <div class="form-floating mb-3">
        <textarea
          type="text"
          class="form-control"
          :class="validationArticle && 'validation'"
          v-model="article"
        />
        <label>Article</label>
      </div>

      <button
        class="w-100 btn btn-lg btn-primary"
        type="submit"
        @click="addArticle"
      >
        Submit
      </button>
      <hr class="my-4">
      <span
        v-if="articleAdded"
        class="alert-success p-2 d-flex justify-content-center"
      >
        Article has added
      </span>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  data() {
    return {
      title: '',
      article: '',
      articleAdded: false,
      validationTitle: false,
      validationArticle: false,
    }
  },
  methods: {
    validation() {
      this.validationTitle = false
      this.validationArticle = false
      if (this.title === '') {
        this.validationTitle = true
      }
      if (this.article === '') {
        this.validationArticle = true
      }
      return this.validationTitle || this.validationArticle
    },
    addArticle(e) {
      e.preventDefault()
      if (this.validation()) {
        return
      }
      this.$emit('addArticle', {
        title: this.title,
        body: this.article,
      })
      this.title = ''
      this.article = ''
      this.articleAdded = true
      setTimeout(() => {
        this.articleAdded = false
      }, 3000)
    }
  },
}
</script>

<style scoped>
 .validation {
   border: solid 1px red;
 }
</style>
