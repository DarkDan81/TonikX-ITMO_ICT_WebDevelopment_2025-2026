<template>
  <v-container class="justify-center d-flex">
    <v-card width="600" class="pa-6">
      <h2 class="text-h5 mb-6"><v-icon icon="mdi-upload" color="primary" class="mr-2"></v-icon>Сдать работу</h2>
      <v-select v-model="selectedVariant" :items="variants" item-title="description" item-value="id" label="Вариант"></v-select>
      <v-textarea v-model="content" label="Ссылка на решение" rows="4"></v-textarea>
      <v-btn block color="primary" size="large" class="mt-6" @click="submitWork">Отправить</v-btn>
    </v-card>
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  data: () => ({ variants: [{id: 1, description: "Вариант №1"}], selectedVariant: null, content: '' }),
  methods: {
    async submitWork() {
      const token = localStorage.getItem('auth_token');
      try {
        await axios.post('http://127.0.0.1:8000/api/submissions/', 
          { variant: this.selectedVariant, content: this.content },
          { headers: { Authorization: `Token ${token}` } }
        );
        alert('Сдано!');
      } catch (e) { alert('Ошибка'); }
    }
  }
}
</script>