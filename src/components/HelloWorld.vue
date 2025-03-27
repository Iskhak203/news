<script setup>
import { ref,onMounted } from "vue";

const total = ref(100)
// const activeBox = ref(null)
const boxList = ref([])
const mBoxes = ref([]); 

const Colors = ["red", "blue", "black", "green", "yellow", "Purple", "Teal"];

const initArr = () => {
  boxList.value = [];
  mBoxes.value = []; 
  for (let i = 0; i < total.value; i++) {
    boxList.value.push({
      id: new Date().getTime() + i,
      label: Math.floor(Math.random() * 100),
      color: Colors[Math.floor(Math.random() * Colors.length)],
    });
  }
};

// const bor=(num)=>{
//   total.value=num;
//   initArr()
// }
const upBox = (index) => {
  const sBox = boxList.value[index];
  mBoxes.value.push(sBox);
  boxList.value.splice(index, 1);
 
};
const pushBox = (index) =>{
 const sBox2 = mBoxes.value[index]
 boxList.value.push(sBox2)
 mBoxes.value.splice(index,1)
}

onMounted(()=>{
  initArr()

})



</script>

<template>
  <input type="text" v-model="total" @change="initArr">
  <div class="box_container">
    <div 
      v-for="(box , index) in boxList" :key="box.id"
      class="box" 
      :class="{'red': box.selected}" 
      :style="{ backgroundColor: box.color }" 
        @click="upBox(index)"
    >
      {{ box.label }}
    </div>
  </div>
  <hr>
  <!-- <h1>------------------------------------------------------------------------------------------------------------------------------------------------------------</h1> -->
  <div class="box_container">
    <div 
      v-for="(box  , index) in mBoxes" 
      :key="box.id"
      class="box"
      :style="{ backgroundColor: box.color }"
      @click="pushBox(index)"
    >
      {{ box.label }}
    </div>
  </div>
</template>

<style scoped>
  .box_container{
    display: flex;
    flex-wrap: wrap;
  }
  .box {
    background-color: rgb(79, 79, 208);
    width: 40px;
    height: 40px;
    margin: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    font-weight: bold;
    cursor: pointer;
  }
  .red{
    background-color: rgb(255, 69, 69);
  }

</style>