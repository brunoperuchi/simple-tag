<template>
  <div class="make-tag">
    <h2>Cria crachá</h2>
    <button @click="showTagModel = true">Inserir fundo</button>
    <button @click="showPhoto = true">Inserir imagem</button>
    <my-upload field="img"
        @crop-success="uploadTagModel"
        v-model="showTagModel"
        :width="300"
        :height="400"
        :langExt="langExt"
        :noCircle="true"
        :noSquare="true" />
    <my-upload field="img"
        @crop-success="uploadPhoto"
        v-model="showPhoto"
        :width="300"
        :height="400"
        :langExt="langExt"
        :noCircle="true"
        :noSquare="true" />
    <input type="text" v-model="name" placeholder="Nome">
    <textarea v-model="role" placeholder="Função" />
    <div class="result">
      <div class="tag" :style="`background-image: url(${tagModel})`">
        <img v-if="photo" :src="photo">
        <h2>Nome:</h2>
        <h3>{{name}}</h3>
        <h2>Função:</h2>
        <h3 style="white-space: pre-line;">{{role}}</h3>
      </div>
    </div>
  </div>
</template>

<script>
import MyUpload from 'vue-image-crop-upload';

export default {
  components: {
    MyUpload
  },

  data() {
    return{
      tagModel: null,
      photo: null,
      name: "",
      role: "",
      showTagModel: false,
      showPhoto: false,
      langExt: {
        hint: 'Click or drag the file here to upload',
        loading: 'Uploading…',
        noSupported: 'Browser is not supported, please use IE10+ or other browsers',
        success: 'Upload success',
        fail: 'Upload failed',
        preview: 'Preview',
        btn: {
          off: 'Cancel',
          close: 'Close',
          back: 'Back',
          save: 'Save'
        },
        error: {
          onlyImg: 'Image only',
          outOfSize: 'Image exceeds size limit: ',
          lowestPx: 'Image\'s size is too low. Expected at least: '
        }
      }
    }
  },

  methods: {
    uploadTagModel(imageDataUrl) {
      this.tagModel = imageDataUrl
    },

    uploadPhoto(imageDataUrl) {
      this.photo = imageDataUrl
    }
  }
}
</script>

<style scoped>
.make-tag {
  display: flex;
  flex-flow: wrap column;
}

.tag {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 600px;
  height: 800px;
  background-size: contain;
}
</style>