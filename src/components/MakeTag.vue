<template>
  <div class="make-tag">
    <h1 class="header">Simple Tag</h1>
    <button @click="showTagModel = true">Inserir Moldura</button>
    <button @click="showPhoto = true">Inserir Foto</button>
    <my-upload field="img"
        @crop-success="uploadTagModel"
        v-model="showTagModel"
        :width="550"
        :height="860"
        :langExt="langExt"
        :noCircle="true"
        :noSquare="true" />
    <my-upload field="img"
        @crop-success="uploadPhoto"
        v-model="showPhoto"
        :width="195"
        :height="266"
        :langExt="langExt"
        :noCircle="true"
        :noSquare="true" />
    <input type="text" v-model="name" placeholder="Nome">
    <input type="text" v-model="role" placeholder="Função" />
    <div ref="tag" class="tag" :style="`${tagModel ? `background-image: url(${tagModel})`: ''}`">
      <img class="photo" v-if="photo" :src="photo">
      <div class="text">
        <p class="name">{{name}}</p>
        <p class="role">{{role}}</p>
      </div>
    </div>
    <button @click="downloadPDF">Gerar PDF</button>
  </div>
</template>

<script>
import MyUpload from 'vue-image-crop-upload';
import jsPDF from 'jspdf';
import html2canvas from 'html2canvas';

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
    },

    downloadPDF() {
      html2canvas(this.$refs.tag).then((canvas) => {        
        const pdf = new jsPDF('p', 'mm', [55, 86])

        pdf.addImage(canvas, 'JPEG', 0, 0, 55, 86, '', 'SLOW')

        pdf.save('test.pdf')
      })
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

* {
  font-family: 'Roboto', sans-serif;
  text-align: center;
  color:#000
}

.make-tag {
  background: #313131;
  padding: 10px;
  border-radius: 10px;
  margin: auto;
  display: grid;
  row-gap: 10px;
  grid-template-rows: repeat(5, 1fr) 9fr 1fr;
  max-width: 600px;
  min-width: 210px;
  height: 90vh;
}

.header {
  color: #fff;
}

button {
  border: none;
  background: #727272;
  font-size: 15pt;
  border-radius: 5px;
  font-weight: bold;
}

button:hover {
  background: #161616;
  color: #fff;
}

input {
  background: #3d3d3d;
  color: #fff;
  border: none;
  border-radius: 5px;
  outline: none;
  text-align: center;
  font-size: 15pt;
}

.tag {
  margin: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-size: contain;
  width: 55mm;
  height: 85mm;
}

.photo {
  margin-top: 26.6mm;
  width: 19.5mm;
  height: 26.6mm;
  border: solid 1px #000;
}

.text {
  font-weight: bold;
}

.name {
  font-size: 12pt;
}

.role {
  font-size: 9pt;
}
</style>