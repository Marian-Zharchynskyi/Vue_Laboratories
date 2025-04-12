<script setup lang="ts">
import { ref } from 'vue'

const shoppingList = ref([
  { id: 1, title: 'Курятина 1 кг', bought: false },
  { id: 2, title: 'Молоко 1 л', bought: false },
  { id: 3, title: 'Яйця 10 штук', bought: false },
])

const newItemTitle = ref('')

const doneBought = (id: number) => {
  const item = shoppingList.value.filter((item) => item.id === id)[0]
  if (item) {
    item.bought = !item.bought
  }
}

const deleteItem = (id: number) => {
  shoppingList.value = shoppingList.value.filter((item) => item.id !== id)
}

const addNewItem = () => {
  if (newItemTitle.value.trim()) {
    const newId = shoppingList.value.length
      ? shoppingList.value[shoppingList.value.length - 1].id + 1
      : 1
    shoppingList.value.push({
      id: newId,
      title: newItemTitle.value.trim(),
      bought: false,
    })
    newItemTitle.value = ''
  }
}
</script>

<template>
  <main>
    <div class="pa-6">
      <v-text-field
        v-model="newItemTitle"
        label="Додати елемент"
        append-icon="mdi-plus"
        variant="outlined"
        clearable
        @click:append="addNewItem"
        @keyup.enter="addNewItem"
      />
      <v-list>
        <div v-for="(item, index) in shoppingList" :key="item.id">
          <v-list-item @click="doneBought(item.id)" :class="{ 'blue lighten-5': item.bought }">
            <v-list-item-action>
              <v-checkbox v-model="item.bought"></v-checkbox>
            </v-list-item-action>
            <template v-slot:title>
              <span :class="{ 'text-decoration-line-through': item.bought }">
                {{ item.title }}
              </span>
            </template>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteItem(item.id)">
                <v-icon>mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </v-list-item>
          <v-divider v-if="index < shoppingList.length - 1" :key="'divider-' + item.id" />
        </div>
      </v-list>
    </div>
  </main>
</template>