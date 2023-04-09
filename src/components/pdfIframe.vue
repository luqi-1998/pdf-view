<template>
    <div class="box">
        <el-dialog
    v-model="dialogVisible"
    :fullscreen="false"
    :width="1000"
    :before-close="handleClose"
  >
  <embed type="application/pdf" :src="pdfUrl" width="800" height="600">
    <!-- <iframe :src="pdfUrl" :width="1000" height="600px" frameborder="0"></iframe> -->
    </el-dialog>
    </div>
</template>
<script setup>
import { reactive, onMounted, computed } from "vue";
const props = defineProps({
    pdfUrl: {
        type: String,
        required: true
    },
    modelValue:{
        type:Boolean,
        default:false
    }
})
const emit=defineEmits(['update:modelValue'])
const dialogVisible=computed({
    get:()=>{
        return props.modelValue
    },
    set:(value)=>{
      emit('update:modelValue',value)
    }
})



const handleClose=()=>{
  dialogVisible.value=false
}

onMounted(() => {
    
});

</script>

<style lang="css" scoped>
embed{
    -webkit-transform:scale(1);
    -moz-transform:scale(1);
    -o-transform: scale(1);
    -ms-zoom: 1;
}
.box >>> .el-dialog__body{
 padding: 0px !important;
}
.box >>> .el-dialog{
    --el-dialog-margin-top:40px !important;
}
</style>