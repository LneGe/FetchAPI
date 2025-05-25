

<script setup>
import axios from "axios";
import { onMounted, reactive } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();

const postId = route.params.id;
const state = reactive({
  post: Object,
});

onMounted(async () => {
  try {
    const response = await axios.get(
      `http://localhost/belajar-api/get-all-data.php/?id=${postId}`
    );
    state.post = response.data;
  } catch (error) {
    console.log("Error while fetching: ", error);
  }
});
</script>

<template>
  <div class="post-view-container">
    <div class="content">
      <h1 class="title">Post Details</h1>
      <div class="post-details">
        <p><strong>Student No:</strong> {{ state.post.student_no }}</p>
        <p><strong>Student Name:</strong> {{ state.post.student_name }}</p>
        <p><strong>Student Class:</strong> {{ state.post.student_class }}</p>
      </div>
      <RouterLink :to="`/posts`" class="btn btn-green">Return to Posts</RouterLink>
    </div>
  </div>
</template>

<style scoped>
/* Container styling */
.post-view-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(135deg, #252525, #555555);
  color: white;
  text-align: center;
}

/* Content styling */
.content {
  max-width: 600px;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 1rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Title styling */
.title {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 1.5rem;
}

/* Post details styling */
.post-details {
  text-align: left;
  margin-bottom: 2rem;
  font-size: 1.125rem;
  line-height: 1.75rem;
}

.post-details p {
  margin: 0.5rem 0;
}

/* Button styling */
.btn {
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  font-size: 1rem;
  font-weight: 600;
  text-transform: uppercase;
  transition: all 0.3s ease;
  display: inline-block;
  text-decoration: none;
}

.btn-green {
  background-color: #2e7d32;
  color: white;
}

.btn-green:hover {
  background-color: #1b5e20;
  transform: translateY(-2px);
}
</style>
