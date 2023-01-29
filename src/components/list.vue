<!--
 * @Author: ahmr-bot ahmrcxy@gmail.com
 * @Date: 2022-11-24 14:37:22
 * @LastEditors: ahmr-bot ahmrcxy@gmail.com
 * @LastEditTime: 2022-11-27 08:47:45
 * @FilePath: \Friends\Friends\src\components\list.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
    <v-list>
      <v-list-item v-for="list in lists" :prepend-avatar=avatar>
        <v-list-item-tittle>{{ list.name }}</v-list-item-tittle>
      </v-list-item>
    </v-list>
    <v-list>
      <v-list-item prepend-icon="home" title="首页"></v-list-item>
    </v-list>
    <v-divider></v-divider>
    <v-list>
      <v-list-item prepend-icon="home" href="" title="页面"></v-list-item>
    </v-list>
</template>
<script setup>
import axios from 'axios';
import { ref } from 'vue';
const avatar = './favicon.ico'
console.log(avatar)
const lists = ref([])
axios({
  method:'get',
  url:'./list.json'
}).then((res)=>{
  console.log(res.data.links)
  lists.value = res.data
})
</script>