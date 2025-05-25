

<script setup>
import { onMounted, reactive } from "vue";
import { RouterLink } from "vue-router";
import axios from "axios";
import Post from "@/components/Post.vue";

const state = reactive({
  posts: [],
});

onMounted(async () => {
  try {
    const response = await axios.get(
      "http://localhost/belajar-api/get-all-data.php"
    );
    state.posts = response.data;
  } catch (error) {
    console.error("Error fetching posts:", error);
  }
});
</script>

<template>
  <div class="posts-container">
    <div class="content">
      <h1 class="title">All Posts</h1>
      <div class="actions">
        <RouterLink :to="`/home`" class="btn btn-blue">Go to Home</RouterLink>
        <RouterLink :to="`/posts/add`" class="btn btn-green"
          >Add Post</RouterLink
        >
      </div>
      <table class="posts-table">
        <thead>
          <tr>
            <th>No</th>
            <th>Name</th>
            <th>Class</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <Post
            v-for="post in state.posts"
            :key="post.student_id"
            :post="post"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
/* Container styling */
.posts-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #252525, #555555);
  color: white;
  text-align: center;
  padding: 2rem;
}

/* Content styling */
.content {
  max-width: 900px;
  width: 100%;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 1rem;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Title styling */
.title {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 1.5rem;
}

/* Actions styling */
.actions {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1.5rem;
}

.btn {
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  font-size: 1rem;
  font-weight: 600;
  text-transform: uppercase;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-block;
}

.btn-blue {
  background-color: #1976d2;
  color: white;
}

.btn-blue:hover {
  background-color: #1565c0;
  transform: translateY(-2px);
}

.btn-green {
  background-color: #2e7d32;
  color: white;
}

.btn-green:hover {
  background-color: #1b5e20;
  transform: translateY(-2px);
}

/* Table styling */
.posts-table {
  width: 100%;
  border-collapse: collapse;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 0.5rem;
  overflow: hidden;
}

.posts-table th,
.posts-table td {
  padding: 1rem;
  text-align: center;
  color: white;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
}

.posts-table th {
  background-color: rgba(0, 0, 0, 0.2);
  font-weight: bold;
}

.posts-table tr:hover {
  background-color: rgba(255, 255, 255, 0.1);
}
</style>
