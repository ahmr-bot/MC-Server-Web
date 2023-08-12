<template>
  <v-app id="inspire">
    <!--appbar-->
    <v-app-bar v-for="list in lists" color="primary">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>{{ list.name }} 官网</v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" expand-on-hover rail permanent>
      <List />
    </v-navigation-drawer>
    <!--appbarend-->
    <v-main>
      <v-container>

        <template v-for="n in 1" :key="n">
          <v-card    v-for="list in lists">
            <v-img
            cover
            height="300"
        :src="list.img"
      ></v-img>
      <v-card-title class="text-h6" >{{ list.name }}</v-card-title>
      <v-card-text>{{ list.description }}</v-card-text>
          </v-card>
          <br />
          <v-card  text="图片……">
            <v-row
      class="mb-6"
      no-gutters
      v-for="img in imgs"
    >
            <v-col  cols="4.5">
            <v-img :src="img.leftsrc">
            </v-img>
          </v-col>
            <v-col
        cols="4.5"
        offset="4.5"
      >
            <v-img :src="img.rightsrc">
            </v-img>
          </v-col>
          </v-row>
          </v-card>
            <v-card v-for="list in lists" text="在线状态">
              <v-card-text>
            <div>服务器地址: <strong>{{ list.address }}</strong></div>
            <div>服务器状态: <strong>{{ status.status }}</strong></div>
            <div>服务器在线人数：<strong>{{ status.players }}</strong></div>
          </v-card-text>
          </v-card>
          <br />
          <v-card v-for="list in lists" text="加入服务器">
          <v-card-text>
            <div @click="copy(list.address)">服务器 IP: <strong>{{ list.address }}</strong>←点我复制</div>
            <div>{{ list.teachzb }}</div>
            <div>{{ list.teachwz }}</div>
            <v-btn :href="list.skin"  color="primary">镜缘皮肤站</v-btn><br />
            <v-btn :href="list.grouplink"  color="primary">加入 QQ 群</v-btn>
          </v-card-text>
          </v-card>
          <copyright />
        </template>

      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import axios from 'axios';
import { ref } from 'vue';
import copyright from './copyright.vue';
import List from './list.vue';
function copy(text) {
  navigator.clipboard.writeText(text)
}
const lists = ref([])
const imgs = ref([])
axios({
  method:'get',
  url:'./list.json'
}).then((res)=>{
  console.log(res.data)
  lists.value = res.data
})
axios({
  method:'get',
    url:'./imgs.json'
}).then((res)=>{
  console.log(res.data)
  imgs.value = res.data
})
const status = ref([])
axios({
  method:'get',
  url: "https://uapis.cn/api/mcserver?server=gloxina.top&port=25565",
}).then((res)=>{
  console.log(res.data.status)
  status.value = res.data
})
</script>
<script>
export default {
  data: () => ({ drawer: 111 }),
}
</script>
