<script setup>
import { ref, onMounted,onUnmounted } from 'vue';

const graph = ref([])
const intervalId = null;

const generateGraph = () => {
  graph.value = []; 
  for (let i = 0; i < 20; i++) {
    graph.value.push(Math.random() * 100);
  }
};
const resetGraph =()=>{
    graph.value.shift();
    graph.value.push(Math.random()*100);
}

onMounted(() =>{
generateGraph();
intervalId = setInterval(resetGraph, 300)
}); 
onUnmounted(() => {
  clearInterval(intervalId);
});

</script>



<template>
<div class="container">
<div class="graph_block">
  <div 
    class="item" 
    v-for="item in graph" 
    :style="{'height': item+'%'}"
  >
  {{ Math.random(height) }}
  </div>
</div>

</div>
</template>


<style scoped>
.graph_block{
  display: flex;
  height: 200px;
  align-items: flex-end;
}
.item{
  height: 100%;
  width: 20px;
  margin: 4px;
  background-color: #2892ff;
}
.center{
  text-align: center;
  margin-bottom: 1rem;
}

</style>