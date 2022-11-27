<!--
 * @Author: ahmr-bot ahmrcxy@gmail.com
 * @Date: 2022-11-27 09:51:15
 * @LastEditors: ahmr-bot ahmrcxy@gmail.com
 * @LastEditTime: 2022-11-27 21:41:36
 * @FilePath: \MC\src\components\copyright.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
    <v-footer>
        <v-col  class="text-center" >
        版权所有 © {{ new Date().getFullYear() }} — <strong href="https://aehxy.com">Aehxy</strong>
        </v-col></v-footer>
        <v-footer v-for="list in lists">
          <v-col class="text-center" href="https://beian.miit.gov.cn">
           {{ list.icp  }}
          </v-col>
        </v-footer>
</template>
<script setup>
import { ref } from 'vue'
import axios from 'axios'
const lists = ref([])
axios({
  method:'get',
  url:'./list.json'
}).then((res)=>{
  console.log(res.data.lists)
  lists.value = res.data
})
</script>