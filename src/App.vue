<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" :prepend-icon="item.icon">
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
            <v-list-item-subtitle>Details for {{ item.title }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app fixed elevation="0" class="bg-image">
      <v-app-bar-nav-icon variant="text" @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title>Lab2</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script setup>
import {ref} from 'vue'

const drawer = ref(true)
const items = ref([
  {title: 'List', icon: 'mdi-format-list-checks', to: '/'},
  {title: 'Contact', icon: 'mdi-email', to: '/about'}
])
</script>

<style scoped>
.v-app-bar.bg-image {
  background-image: url('https://picsum.photos/1920/1080?random');
  background-size: cover;
  background-position: center;
  height: 64px;
}
</style>