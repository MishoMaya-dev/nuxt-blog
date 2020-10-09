<template>
    <el-card
      class="post"
      shadow="hover"
      :body-style="{ padding: 0 }"
    >
      <header
        slot="header"
        class="post-header"
      >
        <h1>Post title</h1>
        <small>
          <i class="el-icon-time" />
          {{ new Date().toLocaleString() }}
        </small>
      </header>
      <div class="post-body">
        <img
          src="https://1wine.ru/media/degustation_photo/88/33/chto-delat-gastronomicheskomu-turistu-na-ostrove-phuket.jpg"
          alt="post image"
          class="post-img"
        />
      </div>
      <footer class="post-footer">
        <el-button
          round
          @click="openPost"
        >
          Открыть
        </el-button>
        <span>
          <i class="el-icon-message"/>
          12
        </span>
      </footer>
    </el-card>
</template>

<script>
  export default {
    name: "Post",
    methods: {
      openPost() {
        this.$router.push('/post/test')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .post {
    margin-bottom: 1rem;
  }
  .post-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .post-img {
    width: 100%;
    height: auto;
  }
  .post-footer {
    padding: 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
