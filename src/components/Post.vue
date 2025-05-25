

<script setup>
import axios from "axios";
import { defineProps } from "vue";
import { RouterLink, useRouter } from "vue-router";

const router = useRouter();

const props = defineProps({
  post: Object,
});

const deletePost = async (deletedId) => {
  try {
    const confirm = window.confirm(
      "Are you sure you want to delete this posts?"
    );
    if (confirm) {
      const res = await axios.delete(
        `http://localhost/belajar-api/delete-data.php?student_id=${deletedId}`
      );
      console.log("Delete success:", res.data);
      router.push("/");
    }
  } catch (error) {
    console.error(
      "Error deleting post: ",
      error.response?.data || error.message
    );
  }
};
</script>
<template>
  <tr>
    <td>{{ post.student_no }}</td>
    <td>{{ post.student_name }}</td>
    <td>{{ post.student_class }}</td>
    <td>
      <RouterLink :to="`/posts/${post.student_id}`" class="btn btn-green"
        >View</RouterLink
      >
      <RouterLink :to="`/posts/edit/${post.student_id}`" class="btn btn-blue"
        >Update</RouterLink
      >
      <button @click="deletePost(post.student_id)" class="btn btn-red">
        Delete
      </button>
    </td>
  </tr>
</template>
<style scoped>

.btn {
  padding: 0.75rem 1rem;
  margin-left: 0.5rem;
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

.btn-red {
  background-color: #e53935;
  color: white;
}

.btn-red:hover {
  background-color: #b71c1c;
  transform: translateY(-2px);
}
</style>