<template>
    <el-form
      :model="controls"
      :rules="rules"
      ref="form"
      @submit.native.prevent="onSubmit"
    >
      <h1 class="mb">Создать новый пост</h1>
      <el-form-item
        label="Введите название поста"
        prop="title"
      >
        <el-input
          type="title"
          v-model.trim="controls.title"
        />
      </el-form-item>

      <el-form-item
      label="Текст в формате .mb или .html"
      prop="text"
    >
      <el-input
        type="textarea"
        v-model="controls.text"
        rows="10"
        resize="none"
      />
      </el-form-item>
      <el-button
        class="mb"
        type="success"
        plain
        @click="previewDialog = true"
      >
        Предпросмотр
      </el-button>
      <el-dialog title="Предпросмотр" :visible.sync="previewDialog">
        <div :key="controls.text">
          <vue-markdown>
            {{ controls.text }}
          </vue-markdown>
        </div>
      </el-dialog>
      <el-upload
        class="mb"
        ref="upload"
        drag
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-change="handleImageChange"
        :auto-upload="false"
      >
        <i class="el-icon-upload"></i>
        <div class="el-upload__text">Перетащите картинку или <em>нажмите для загрузки</em></div>
        <div class="el-upload__tip" slot="tip">файлы с расширением jpg/png</div>
      </el-upload>
      <el-form-item>
        <el-button
          type="primary"
          native-type="submit"
          :loading="loading"
          round
        >
          Создать пост
        </el-button>
      </el-form-item>
    </el-form>
</template>

<script>
  export default {
    name: 'create',
    layout: 'admin',
    middleware: ['admin-auth'],
    data: () => ({
      previewDialog: false,
      loading: false,
      controls: {
        text: '',
        title: '',
        image: null
      },
      rules: {
        title: [
          { required: true, message: 'Название поста не может быть пустым', trigger: 'blur' }
        ],
        text: [
          { required: true, message: 'Текст не должен быть пустым', trigger: 'blur' }
        ]
      }
    }),
    methods: {
      handleImageChange(file, fileData) {
        this.image = file.raw
      },
      onSubmit() {
        this.$refs.form.validate( async valid => {
          if (valid && this.image) {
            this.loading = true
            const formData = {
              title: this.controls.title,
              text: this.controls.text,
              image: this.controls.image
            }
            try {
              await this.$store.dispatch('post/create', formData)
              this.controls.title = ''
              this.controls.text = ''
              this.controls.image = null
              this.$refs.upload.clearFiles()
              this.$message.success(`Пост создан`)
            } catch (e) {
            } finally {
              this.loading = false
            }
          } else {
            this.$message.warning('Форма не валидна')
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
