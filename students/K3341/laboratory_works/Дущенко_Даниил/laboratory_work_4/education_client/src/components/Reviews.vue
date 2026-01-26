<template>
  <v-container class="justify-center d-flex">
    <v-card width="600" class="pa-6">
      <h2 class="text-h5 mb-6"><v-icon icon="mdi-star" color="secondary" class="mr-2"></v-icon>Оценить</h2>
      <v-text-field v-model="subId" label="ID Решения"></v-text-field>
      <v-text-field v-model="score" label="Балл (1-5)" type="number"></v-text-field>
      <v-textarea v-model="comment" label="Комментарий" rows="4"></v-textarea>
      <v-btn block color="secondary" size="large" class="mt-6" @click="sendReview">Сохранить</v-btn>
    </v-card>
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  data: () => ({ subId: '', comment: '', score: '' }),
  methods: {
    async sendReview() {
      const token = localStorage.getItem('auth_token');
      await axios.post('http://127.0.0.1:8000/api/reviews/', 
        { submission: this.subId, comments: this.comment, total_score: this.score },
        { headers: { Authorization: `Token ${token}` } }
      );
      alert('Сохранено');
    }
  }
}
</script>