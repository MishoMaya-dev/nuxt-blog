<template>
  <el-menu
    router
    :style="{height: '100%'}"
    :default-active="$route.path"
    background-color="#545c64"
    text-color="#fff"
    active-text-color="#ffd04b"
  >
    <el-menu-item index="/admin">
      <i class="el-icon-data-analysis"></i>
      <span>Аналитика</span>
    </el-menu-item>
    <el-menu-item index="/admin/create">
      <i class="el-icon-document-add"></i>
      <span>Создать</span>
    </el-menu-item>
    <el-menu-item index="/admin/list">
      <i class="el-icon-files"></i>
      <span>Посты</span>
    </el-menu-item>
    <el-menu-item index="/admin/users">
      <i class="el-icon-user"></i>
      <span>Пользователи</span>
    </el-menu-item>
    <el-menu-item index="/admin/logout">
      <i class="el-icon-unlock"></i>
      <span>Выйти</span>
    </el-menu-item>
  </el-menu>
</template>

<script>
    export default {
        name: "Aside"
    }
</script>

<style scoped>

</style>
