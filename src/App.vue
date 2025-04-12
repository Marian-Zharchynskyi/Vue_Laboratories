<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          :prepend-icon="item.icon"
        >
          <template v-slot:title> {{ item.title }} </template>
          <template v-slot:subtitle> Details for {{ item.title }}</template>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app fixed color="transparent" elevation="0" class="bg-image">
      <v-app-bar-nav-icon variant="text" @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title>Lab2</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const drawer = ref(true)

const items = [
  { title: 'List', icon: 'mdi-format-list-checks', to: '/' },
  { title: 'About us', icon: 'mdi-email', to: '/about' },
  { title: 'My group', icon: 'mdi-account-group', to: '/my-group' },
]
</script>

<style scoped>
.v-app-bar.bg-image {
  background-image: url('https://picsum.photos/1920/1080?random');
  background-size: cover;
  background-position: center;
  height: 64px;
}
</style>
