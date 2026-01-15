<template>
  <v-app>
    <v-app-bar elevation="0" color="surface" class="border-b">
      <v-container class="d-flex align-center py-0">
        <v-icon icon="mdi-school-outline" color="primary" class="mr-3" size="32"></v-icon>
        <v-toolbar-title class="font-weight-bold text-h6">
          ITMO<span class="text-primary">.Edu</span>
        </v-toolbar-title>

        <v-spacer></v-spacer>

        <!-- Меню (скрываем на мобильных, но для лабы сойдет) -->
        <div class="d-flex ga-2">
          <v-btn to="/assignments" variant="text">Задания</v-btn>
          <v-btn to="/submit" variant="text">Сдать работу</v-btn>
          <v-btn to="/reviews" variant="text">Проверки</v-btn>
          <v-btn @click="logout" icon color="grey-lighten-1">
            <v-icon>mdi-logout-variant</v-icon>
          </v-btn>
        </div>
      </v-container>
    </v-app-bar>

    <v-main class="bg-background">
      <v-container class="py-10">
        <router-view v-slot="{ Component }">
          <transition name="fade" mode="out-in">
            <component :is="Component" />
          </transition>
        </router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  methods: {
    logout() {
      localStorage.removeItem('auth_token');
      this.$router.push('/');
    }
  }
}
</script>

<style>
/* Плавная анимация переходов */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
.border-b {
  border-bottom: 1px solid rgba(255, 255, 255, 0.08) !important;
}
</style>