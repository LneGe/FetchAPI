

<script setup>
import { RouterLink, useRouter } from 'vue-router';

const router = useRouter();

function handleLogout() {
  localStorage.removeItem('user');
  router.push('/'); // pastikan route '/login' mengarah ke PostsLogin.vue
}
</script>

<template>
  <div class="home-container">
    <div class="content">
      <h1 class="title">Selamat datang di FetchJSON</h1>
      <hr><br>
      <div class="actions">
        <RouterLink :to="`/posts`" class="btn btn-green">Go To Posts</RouterLink>
        <button class="btn btn-red" @click="handleLogout">Logout</button>
      </div>
    </div>
  </div>
</template>

<style scoped>

.home-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #252525, #555555);
  color: white;
  text-align: center;
  padding: 2rem;
}

.content {
  max-width: 500px;
  width: 100%;
  background: rgba(255,255,255,0.12);
  border-radius: 1rem;
  padding: 2.5rem 2rem;
  box-shadow: 0 4px 16px rgba(0,0,0,0.08);
  color: #222;
}

.title {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  color: #FFFFFF;
}

.subtitle {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  color: #333;
}

.actions {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.btn {
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  font-size: 1rem;
  font-weight: 600;
  text-transform: uppercase;
  transition: all 0.3s ease;
  display: inline-block;
  text-decoration: none;
  border: none;
  cursor: pointer;
}

.btn-green {
  background-color: #2e7d32;
  color: white;
}

.btn-green:hover {
  background-color: #1b5e20;
  transform: translateY(-2px);
}

.btn-red {
  background-color: #e53935;
  color: white;
}

.btn-red:hover {
  background-color: #b71c1c;
  transform: translateY(-2px);
}
</style>