<template>
 <div class="loading-overlay" v-if="loadingVisible">
 <div class="progress-bar-container">  
<div class="progress-circle" id="progress1" style="margin-left:50px">
      <el-progress 
      :percentage="loadingMON_bar" 
      :stroke-width="10" 
      :show-text="false" 
      style="width:100%;display:flex">
      </el-progress>
  </div>
 <div class="progress-bar" id="progress2" style="margin-left:-6px;margin-top: -19px;margin-bottom: auto; ">
      <el-progress 
      :percentage="loadingMON_circle" 
      type="circle"
      :stroke-width="15" 
      :text-inside="true" 
      style="width:100%;display:flex">
      </el-progress>
      <p class="tips_css">MON</p>
</div>
<div class="progress-circle" id="progress3" style="margin-left:-6px;margin-bottom: auto;">
      <el-progress 
      :percentage="loadingMGR_bar" 
      :stroke-width="10" 
      :text-inside="true" 
      :show-text="false" 
      style="width:100%;display:flex">
      </el-progress>
</div>
 <div class="progress-bar" id="progress4" style="margin-left: -6px; margin-top: -19px; margin-bottom: auto; ">
      <el-progress 
      :percentage="loadingMGR_circle" 
      type="circle"
      :stroke-width="15" 
      :text-inside="true" 
      style="display:flex">
      </el-progress>
      <p class="tips_css">MGR</p>
</div>
<div class="progress-circle" id="progress5" style="margin-left:-6px;margin-bottom: auto; ">
      <el-progress 
      :percentage="loadingOSD_bar" 
      :stroke-width="10" 
      :text-inside="true" 
      :show-text="false" 
      style="width:100%;display:flex">
      </el-progress>
</div>
 <div class="progress-bar" id="progress6" style="margin-left: -6px; margin-top: -19px; margin-bottom: auto; ">
      <el-progress 
      :percentage="loadingOSD_circle" 
      type="circle"
      :stroke-width="15" 
      :text-inside="true" 
      style="display:flex">
      </el-progress>
      <p class="tips_css">OSD</p>
</div>
<div v-if="mdsData.length" class="progress-circle" id="progress7" style="margin-left:-6px;margin-bottom: auto; ">
      <el-progress 
      :percentage="loadingMDS_bar" 
      :stroke-width="10" 
      :text-inside="true" 
      :show-text="false" 
      style="width:100%;display:flex">
      </el-progress>
</div>
 <div v-if="mdsData.length" class="progress-bar" id="progress6" style="margin-left: -6px; margin-top: -19px; margin-bottom: auto; z-index: 2;">
      <el-progress 
      :percentage="loadingMDS_circle" 
      type="circle"
      :stroke-width="15" 
      :text-inside="true" 
      style="display:flex">
      </el-progress>
      <p class="tips_css" >MDS</p>
</div>
<div class="progress-circle" id="progress7" style="margin-left:-6px;margin-bottom: auto;margin-right:50px z-index: 1;">
      <el-progress 
      :percentage="loadingend_bar" 
      :stroke-width="10" 
      :text-inside="true" 
      :show-text="false" 
      style="width:100%;display:flex">
      </el-progress>
</div>
 </div>
</div>
<el-button @click="loadingVisibleform">
开始加载
</el-button>
<el-button @click="speedup">
加速
</el-button>
</template>

<script lang="ts" setup>
import { ref, watch, reactive,computed } from 'vue'
import { ElLoading} from 'element-plus'
const loadingVisible = ref(false)
const mdsData = reactive([])
const speedup = () =>{
loadingPercentage.value += 5 
console.log(loadingPercentage.value)
}
const loadingVisibleform = ()=>{
loadingVisible.value = true
}
let loadingPercentage = ref(0)

let loadingMON_bar = ref(0)
let loadingMON_circle = ref(0)
let loadingMGR_bar = ref(0)
let loadingMGR_circle = ref(0)
let loadingOSD_bar = ref(0)
let loadingOSD_circle = ref(0)
let loadingMDS_bar = ref(0)
let loadingMDS_circle = ref(0)
let loadingend_bar = ref(0)

let change_number = ref(0)

const test2 = computed({
  get(){
    return loadingMON_bar.value+=1
  },
  set(){
    loadingMON_bar.value = loadingMON_bar.value
  }

})

watch(change_number,(oldvalue, newvalue)=>{
  if(change_number.value == 1){
  loadingMON_bar.value = 100
  loadingMON_circle.value = 1
  }else if(change_number.value == 2){
    loadingMON_circle.value = 100
    loadingMGR_bar.value = 1
  }
})

watch(loadingMON_circle,(oldvalue, newvalue)=>{
  if(loadingMON_bar.value == 100 && loadingMON_circle.value< 90){
  loadingMON_circle.value += 1
  }
})

setInterval(()=>{
  if(change_number.value != 1 && loadingMON_bar.value < 100){
    loadingMON_bar.value += 1
  }

},50)

setInterval(()=>{
console.log(change_number.value)
  if(loadingMON_bar.value == 80){
    change_number.value = 1
  }else if(loadingMON_circle.value == 0){
  change_number.value = 2
  }
},200)


</script>
<style>
.progress-1{
  display: flex;
  justify-content: space-between;
}

.loading-overlay {
  flex-direction: column;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;  
  align-items: left;
  z-index: 9999;
}
.loading-overlay .progress-bar .el-progress.el-progress--circle.el-progress--text-inside .el-progress-circle {
height:50px !important;
width:50px !important;
}
::v-deep .el-progress__text{
  font-size: 24px !important;
  color: rgb(30, 160, 225) !important;
}
::v-deep .el-progress-bar{
  width: 250px !important;
  height: 150px !important;
}
::v-deep .el-progress-bar__{
  width: 350px !important;
  height: 150px !important;
}
.tips_css{
  margin-top: 0px;
  margin-left: auto;
  font-size: 22px;
  color: rgb(30, 160, 225)
}
.progress-bar-container {  
  display: flex;  
  justify-content: left;  
}  
  
.progress-circle {  
  height: 100%;
  width: 30%;  
  transition: width 0.5s ease;  
}

</style>
