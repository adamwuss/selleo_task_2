<template>
  <div class="px-4 py-5 my-5 text-center">
    <span class="title-article display-5 fw-bold">
      {{ article.title }}
    </span>
    <span class="d-block lead">
      {{ article.body }}
    </span>
    <div class="d-flex justify-content-center gap-2 mt-3">
      <BIconHandThumbsUp
        class="cursor-pointer me-2 text-success"
        @click="$emit('addLike', article.id)"
      />
      <BIconHandThumbsDown
        class="cursor-pointer me-2 text-danger"
        @click="$emit('subtractLike', article.id)"
      />
      <span class="me-5">{{ article.likeCount }}</span>
    </div>
    <div class="d-flex mt-2">
      <button
        class="btn btn-danger mb-3 mt-3 d-grid gap-2 col-2 mx-auto"
        @click="$emit('deleteArticle', article.id)"
      >
        Delete article
      </button>
    </div>
  </div>
</template>

<script>
import { BIconHandThumbsUp, BIconHandThumbsDown, BIconXCircle } from 'bootstrap-vue'

export default {
  name: 'Article',
  emits: ['addLike', 'subtractLike', 'deleteArticle'],
  comments: {
    BIconHandThumbsUp,
    BIconHandThumbsDown,
    BIconXCircle,
  },
  props: {
    article: {
      type: Object,
      default: () => {},
    }
  }
}
</script>

<style scoped>
  .title-article {
    padding-bottom: 0.5rem;
  }
  .cursor-pointer {
    cursor: pointer;
  }
</style>