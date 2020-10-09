<template>
  <el-card class="comment">
    <div class="comment-header">
      <span>Person name</span>
      <span>
        <i class="el-icon-time" />
        {{ new Date().toLocaleString() }}
      </span>
    </div>
    <div class="comment-text">
      Lorem ipsum dolor sit amet.
    </div>
  </el-card>
</template>

<script>
  export default {
    name: 'Comment',
    props: ['comment']
  }
</script>

<style lang="scss" scoped>
  .comment {
   margin-bottom: 1rem
 }
  .comment-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 0.8rem;
    margin-bottom: .5rem;
  }
  .comment-text {
    white-space: pre-line;
  }
</style>
