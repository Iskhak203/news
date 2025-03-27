<script setup>
import {computed, onMounted, ref} from 'vue'

const text = ref('')

const userList = ref([])
const filter = ref('all')

const getUserList = ()=>{
  fetch('https://dummyjson.com/users')
  .then(res => res.json())
  .then(data => userList.value = data.users)
}

const filterUsers = computed(()=>{
  if (filter.value=='all') return searchUser.value
  if (filter.value=='age20') return searchUser.value.filter(el=>el.age>30)
  if (filter.value=='female') return searchUser.value.filter(el=>el.gender=='female')
  if (filter.value=='male') return searchUser.value.filter(el=>el.gender=='male')
})

const searchUser = computed(()=>{
  return userList.value.filter(el=>el.lastName.toLowerCase().includes(text.value.toLowerCase()))
})

onMounted(async()=>{
 await getUserList()
})

</script>

<template>
  <div class="container  flex-column h-100 pt-5">
    <h1 class="text-center">table</h1>
    <input type="text" class="form-control mb-3 mt-3 " v-model="text" @input="searchUser">
    <button class="btn btn-primary me-3" @click="filter='all'">Все</button>
    <button class="btn btn-outline-success me-3" @click="filter='age20'">>20</button>
    <button class="btn btn-primary me-3" @click="filter='female'">female</button>
    <button class="btn btn-outline-info me-3" @click="filter='male'">male</button>
    <ul>
      <li v-for="user in filterUsers" :key="user.id"> {{ user.firstName }} {{ user.lastName }} - {{ user.age }}-{{ user.gender }} </li>
    </ul>
  </div>
</template>

<style scoped>

</style>