<template>
  <el-form
  :model="controls"
  :rules="rules"
  ref="form"
  @submit.native.prevent="onSubmit"
  >
    <h2>Создать пользователя</h2>
    <el-form-item
      label="Логин"
      prop="login"
    >
      <el-input
        v-model.trim="controls.login"
      />
    </el-form-item>

    <div class="mb2">
      <el-form-item
        label="Пароль"
        prop="password"
      >
        <el-input
          type="password"
          v-model.trim="controls.password"
        />
      </el-form-item>
    </div>

    <el-form-item>
      <el-button
        type="primary"
        native-type="submit"
        :loading="loading"
        round
      >
        Создать
      </el-button>
    </el-form-item>
  </el-form>
</template>

<script>
  export default {
    name: "users",
    layout: 'admin',
    middleware: ['admin-auth'],
    data: () => ({
      loading: false,
      controls: {
        login: '',
        password: ''
      },
      rules: {
        login: [
          { required: true, message: 'Введите логин', trigger: 'blur' }
        ],
        password: [
          { required: true, message: 'Введите пароль', trigger: 'blur' },
          { min: 6, message: 'Пароль должен быть больше 6 символов', trigger: 'blur' }
        ]
      }
    }),
    methods: {
      onSubmit() {
        this.$refs.form.validate(async valid => {
          if (valid) {
            this.loading = true
            const formData = {
              login: this.controls.login,
              password: this.controls.password,
            }
            try {
              await this.$store.dispatch('auth/createUser', formData)
              this.controls.login = ''
              this.controls.password = ''
              this.loading = false
            } catch (e) {
              this.loading = false
            }
          }
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  form {
    width: 600px;
  }
</style>
