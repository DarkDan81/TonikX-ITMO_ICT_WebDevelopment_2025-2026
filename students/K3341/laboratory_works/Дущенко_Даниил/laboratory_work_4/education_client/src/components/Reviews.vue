<template>
  <v-container class="justify-center d-flex">
    <v-card width="600" class="pa-6">
      <h2 class="text-h5 mb-6 d-flex align-center">
        <v-icon icon="mdi-fountain-pen-tip" color="secondary" class="mr-3"></v-icon>
        Peer Review
      </h2>
      <p class="text-body-2 text-medium-emphasis mb-4">
        Оцените работу другого студента по критериям.
      </p>

      <v-text-field 
        v-model="subId" 
        label="ID Решения" 
        prepend-inner-icon="mdi-pound"
        placeholder="Например: 1"
      ></v-text-field>

      <v-row>
        <v-col cols="12" sm="4">
           <v-text-field 
            v-model="score" 
            label="Балл (1-5)" 
            type="number" 
            prepend-inner-icon="mdi-star-outline"
          ></v-text-field>
        </v-col>
      </v-row>
      
      <v-textarea 
        v-model="comment" 
        label="Ваш комментарий" 
        placeholder="Опишите сильные и слабые стороны..."
        rows="4"
      ></v-textarea>
      
      <v-btn block color="secondary" size="large" class="mt-6" @click="sendReview">
        Сохранить рецензию
      </v-btn>
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
      alert('Рецензия сохранена');
    }
  }
}
</script>