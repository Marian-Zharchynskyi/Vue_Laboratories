<script setup>
import { ref } from 'vue'

const students = ref([
  {
    id: 1,
    name: 'Нестерчук Віталій',
    birthYear: 2005,
    phone: '+380661234567',
    email: 'vitaliy@example.com',
  },
  {
    id: 2,
    name: 'Дмитро Тарасюк',
    birthYear: 2005,
    phone: '+380671234567',
    email: 'dmytro@example.com',
  },
])

const headers = [
  { title: 'ПІП', key: 'name' },
  { title: 'Рік народження', key: 'birthYear' },
  { title: 'Телефон', key: 'phone' },
  { title: 'Email', key: 'email' },
  { title: 'Дії', key: 'actions', sortable: false },
]

const newStudent = ref({
  name: '',
  birthYear: '',
  phone: '',
  email: '',
})

const editedStudent = ref(null)
const dialog = ref(false)
const search = ref('')

const addStudent = () => {
  if (
    newStudent.value.name &&
    newStudent.value.birthYear &&
    newStudent.value.phone &&
    newStudent.value.email
  ) {
    students.value.push({
      id: students.value.length + 1,
      ...newStudent.value,
    })
    newStudent.value = { name: '', birthYear: '', phone: '', email: '' }
  }
}

const editStudent = (item) => {
  editedStudent.value = { ...item }
  dialog.value = true
}

const saveEdit = () => {
  if (!editedStudent.value) return
  const index = students.value.findIndex((s) => s.id === editedStudent.value.id)
  if (index !== -1) {
    students.value[index] = { ...editedStudent.value }
    students.value = [...students.value]
  }
  dialog.value = false
  editedStudent.value = null
}

const deleteStudent = (id) => {
  students.value = students.value.filter((s) => s.id !== id)
}
</script>

<template>
  <div class="pa-6">
    <h1>Моя група</h1>

    <v-row class="mb-4">
      <v-col cols="12" sm="3">
        <v-text-field v-model="newStudent.name" label="ПІП" outlined dense></v-text-field>
      </v-col>
      <v-col cols="12" sm="2">
        <v-text-field
          v-model="newStudent.birthYear"
          label="Рік народження"
          outlined
          dense
          type="number"
        ></v-text-field>
      </v-col>
      <v-col cols="12" sm="3">
        <v-text-field v-model="newStudent.phone" label="Телефон" outlined dense></v-text-field>
      </v-col>
      <v-col cols="12" sm="3">
        <v-text-field v-model="newStudent.email" label="Email" outlined dense></v-text-field>
      </v-col>
      <v-col cols="12" sm="1">
        <v-btn color="primary" @click="addStudent">Додати</v-btn>
      </v-col>
    </v-row>

    <v-text-field
      v-model="search"
      label="Пошук"
      prepend-inner-icon="mdi-magnify"
      class="mb-4"
      outlined
      dense
    ></v-text-field>

    <v-data-table :headers="headers" :items="students" :search="search" class="elevation-1">
      <template v-slot:item.actions="{ item }">
        <v-btn icon small @click="editStudent(item)">
          <v-icon>mdi-pencil</v-icon>
        </v-btn>
        <v-btn icon small @click="deleteStudent(item.id)">
          <v-icon>mdi-delete</v-icon>
        </v-btn>
      </template>
    </v-data-table>

    <v-dialog v-model="dialog" max-width="500px">
      <v-card v-if="editedStudent">
        <v-card-title>Редагувати студента</v-card-title>
        <v-card-text>
          <v-text-field v-model="editedStudent.name" label="ПІП" outlined dense></v-text-field>
          <v-text-field
            v-model="editedStudent.birthYear"
            label="Рік народження"
            outlined
            dense
            type="number"
          ></v-text-field>
          <v-text-field v-model="editedStudent.phone" label="Телефон" outlined dense></v-text-field>
          <v-text-field v-model="editedStudent.email" label="Email" outlined dense></v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" @click="saveEdit">Зберегти</v-btn>
          <v-btn @click="dialog = false">Скасувати</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
