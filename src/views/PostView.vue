<script setup>
import { ref, watch } from "vue";
import { useRoute } from "vue-router";

const post = ref({});

const route = useRoute();

watch(
  () => route.params.id,
  async (newId) => {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/posts/${newId}`
    );
    const jsonResponse = await response.json();
    post.value = jsonResponse;
  }
);

const fetchPost = async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${route.params.id}`
  );
  const jsonResponse = await response.json();
  post.value = jsonResponse;
};

fetchPost();
</script>

<template>
  <div class="about">
    {{ post.title }}
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
