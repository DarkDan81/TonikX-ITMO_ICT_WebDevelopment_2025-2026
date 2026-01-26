<template>
  <div>
    <h1 class="text-h4 font-weight-bold mb-6">Задания</h1>
    <v-row>
      <v-col v-for="task in tasks" :key="task.id" cols="12" md="6">
        <v-card class="h-100 d-flex flex-column">
          <v-card-item>
            <template v-slot:prepend><v-icon icon="mdi-code-braces" color="primary"></v-icon></template>
            <v-card-title>{{ task.title }}</v-card-title>
          </v-card-item>
          <v-card-text class="text-medium-emphasis">{{ task.description }}</v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-divider class="my-10"></v-divider>
    <v-card variant="outlined" class="pa-6 border-dashed">
      <h3 class="text-h6 mb-4">Создать задание (Teacher)</h3>
      <v-row>
        <v-col cols="12" md="4"><v-text-field v-model="newTitle" label="Название"></v-text-field></v-col>
        <v-col cols="12" md="8">
          <v-text-field v-model="newDesc" label="Описание">
            <template v-slot:append><v-btn color="primary" @click="createTask">Создать</v-btn></template>
          </v-text-field>
        </v-col>
      </v-row>
    </v-card>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data: () => ({ tasks: [], newTitle: '', newDesc: '' }),
  async mounted() { this.loadTasks(); },
  methods: {
    async loadTasks() {
      const token = localStorage.getItem('auth_token');
      const res = await axios.get('http://127.0.0.1:8000/api/assignments/', {
        headers: { Authorization: `Token ${token}` }
      });
      this.tasks = res.data;
    },
    async createTask() {
      const token = localStorage.getItem('auth_token');
      await axios.post('http://127.0.0.1:8000/api/assignments/', 
        { title: this.newTitle, description: this.newDesc },
        { headers: { Authorization: `Token ${token}` } }
      );
      this.loadTasks();
    }
  }
}
</script>