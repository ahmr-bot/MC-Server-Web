<template>
    <v-footer>
        <v-col  class="text-center" >
        版权所有 © {{ new Date().getFullYear() }} — <strong href="https://aehxy.com">Aehxy</strong>
        </v-col>
    </v-footer>
    <v-footer>
    <v-col class="text-center">
      <a href="https://icp.gov.moe/?keyword=20226999">萌ICP备20226999号</a>
    </v-col>
    </v-footer>
        <v-footer v-for="list in lists">
          <v-col class="text-center" href="https://beian.miit.gov.cn">
           {{ list.icp  }}
          </v-col>
        </v-footer>
</template>
<script setup>
import axios from 'axios';
import { ref } from 'vue';
const lists = ref([])
axios({
  method:'get',
  url:'./list.json'
}).then((res)=>{
  console.log(res.data.lists)
  lists.value = res.data
})
</script>