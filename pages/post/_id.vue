<template>
  <article class="post">
    <header class="post-header">
      <div class="post-title">
        <h1>Post title</h1>
        <nuxt-link to="/">
          <i class="el-icon-back"/>
        </nuxt-link>
      </div>
      <div class="post-info">
        <small>
          <i class="el-icon-time" />
          {{ new Date().toLocaleString() }}
        </small>
        <span>
          <i class="el-icon-view" />
          42
        </span>
      </div>
      <div class="post-img">
        <img
          src="https://1wine.ru/media/degustation_photo/88/33/chto-delat-gastronomicheskomu-turistu-na-ostrove-phuket.jpg"
          alt="post image"
        />
      </div>
    </header>
    <main class="post-content">
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad beatae facere officia quibusdam? Ab doloremque incidunt iusto laboriosam laborum sunt?</p>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad beatae facere officia quibusdam? Ab doloremque incidunt iusto laboriosam laborum sunt?</p>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad beatae facere officia quibusdam? Ab doloremque incidunt iusto laboriosam laborum sunt?</p>
    </main>
    <footer>

      <app-comment-form
        v-if="canAddComment"
        @created="createCommentHandler"
      />

      <div
        class="comments"
        v-if="true"
      >
        <app-comment
          v-for="comment in 4"
          :key="comment"
          :comment="comment"
        />
      </div>
      <div
        class="text-center"
        v-else
      >
        Комментариев нет
      </div>
    </footer>
  </article>
</template>

<script>
  import AppComment from '@/components/main/Comment'
  import AppCommentForm from '@/components/main/CommentForm'
  export default {
    validate({params}) {
      return Boolean(params.id)
    },
    data: () => ({
      canAddComment: true
    }),
    components: {
      AppComment,
      AppCommentForm
    },
    methods: {
      createCommentHandler() {
        this.canAddComment = false
        console.log('Pisos')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .post {
    max-width: 600px;
    margin: 0 auto;
  }
  .post-header {
    margin-bottom: 1.5rem;
  }
  .post-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }
  .post-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .5rem;
  }
  .post-img img{
    width: 100%;
    height: auto;
  }
  .post-content {
    margin-bottom: 2rem;
  }
</style>
