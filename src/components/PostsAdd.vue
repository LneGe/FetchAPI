

<script setup>
import axios from "axios";
import { reactive } from "vue";
import router from "@/router";

const form = reactive({
  student_no: "",
  student_name: "",
  student_class: "",
});

const handleSubmit = async () => {
  const newPost = {
    student_no: form.student_no,
    student_name: form.student_name,
    student_class: form.student_class,
  };
  try {
    const response = await axios.post(
      "http://localhost/belajar-api/insert-data.php",
      newPost
    );
    console.log(response);
    return router.push("/posts");
  } catch (error) {
    console.error("Error on posting data:", error);
  }
};
</script>

<template>
  <div class="add-post-container">
    <div class="content">
      <h1 class="title">Add New Post</h1>
      <form @submit.prevent="handleSubmit" class="form">
        <div class="form-group">
          <label for="no">Student No</label>
          <input
            v-model="form.student_no"
            type="text"
            id="no"
            name="no"
            placeholder="Enter Student No"
            class="input"
          />
        </div>

        <div class="form-group">
          <label for="name">Student Name</label>
          <input
            v-model="form.student_name"
            type="text"
            id="name"
            name="name"
            placeholder="Enter Student Name"
            class="input"
          />
        </div>

        <div class="form-group">
          <label for="class">Student Class</label>
          <input
            v-model="form.student_class"
            id="class"
            name="class"
            placeholder="Enter Student Class"
            class="input"
          />
        </div>

        <button type="submit" class="btn btn-green">Submit</button>
      </form>
      <RouterLink :to="`/posts`" class="btn btn-gray">Return to Posts</RouterLink>
    </div>
  </div>
</template>

<style scoped>
/* Container styling */
.add-post-container {
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

/* Form styling */
.form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

.form-group {
  text-align: left;
}

label {
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  display: block;
}

.input {
  width: 100%;
  padding: 0.75rem;
  border-radius: 0.5rem;
  border: none;
  font-size: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.input:focus {
  outline: none;
  box-shadow: 0 0 0 2px #2e7d32;
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

.btn-gray {
  background-color: #757575;
  color: white;
}

.btn-gray:hover {
  background-color: #616161;
  transform: translateY(-2px);
}
</style>