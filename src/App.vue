<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import { ref } from "vue";
import PDFView from "./components/pdfPreview.vue"
import PDFIframe from "./components/pdfIframe.vue"
const jsPdf=ref('')
const fileList=ref([])
const pdfRef=ref(null)
const pdfViewPopup=ref(false)
const pdfIframePopup=ref(false)
const handleBeforeUpload=(file)=>{
  console.log(file);
  console.log(window.URL.createObjectURL(file));
  // setTimeout(()=>{
    jsPdf.value=window.URL.createObjectURL(new Blob([file], {type: 'application/pdf'}))
    pdfIframePopup.value=true
    // pdfViewPopup.value=true
    // pdfRef.value?.loadingPdf(file)
  // },5000)
    return false
}
const handleSuccess=(file)=>{
  console.log(file);
}
const handleError=(file)=>{
  console.log(file);
}
</script>

<template>
  <el-upload
    v-model:file-list="fileList"
    class="upload-demo"
    action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
    multiple
    :before-upload="handleBeforeUpload"
    before-upload
    :on-success="handleSuccess"
    :on-error="handleError"
    :limit="3"
  >
    <el-button type="primary">Click to upload</el-button>
    <template #tip>
      <div class="el-upload__tip">
        jpg/png files with a size less than 500KB.
      </div>
    </template>
  </el-upload>
   <PDFView v-model="pdfViewPopup" ref="pdfRef" :pdfUrl="jsPdf"/>
   <PDFIframe v-model="pdfIframePopup" ref="pdfRef1" :pdfUrl="jsPdf"/>
  <!-- <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" /> -->
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
