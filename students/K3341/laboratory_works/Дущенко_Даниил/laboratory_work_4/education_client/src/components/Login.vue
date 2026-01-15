<template>
  <v-container class="fill-height justify-center">
    <v-card width="400" class="pa-6">
      <div class="text-center mb-6">
        <v-avatar color="primary" size="64" class="mb-4">
          <v-icon icon="mdi-account-lock" color="white" size="32"></v-icon>
        </v-avatar>
        <h2 class="text-h5 font-weight-bold">Вход в систему</h2>
        <p class="text-medium-emphasis text-body-2 mt-1">Введите ваши учетные данные</p>
      </div>

      <v-form @submit.prevent="login">
        <v-text-field 
          v-model="username" 
          label="Логин" 
          prepend-inner-icon="mdi-email-outline"
        ></v-text-field>
        
        <v-text-field 
          v-model="password" 
          label="Пароль" 
          type="password" 
          prepend-inner-icon="mdi-lock-outline"
        ></v-text-field>
        
        <v-btn block color="primary" size="large" type="submit" class="mt-4">
          Войти
        </v-btn>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  data: () => ({ username: '', password: '' }),
  methods: {
    async login() {
      try {
        const response = await axios.post('http://127.0.0.1:8000/auth/token/login/', {
          username: this.username,
          password: this.password
        });
        localStorage.setItem('auth_token', response.data.auth_token);
        this.$router.push('/assignments');
      } catch (e) {
        alert('Неверный логин или пароль');
      }
    }
  }
}
</script>