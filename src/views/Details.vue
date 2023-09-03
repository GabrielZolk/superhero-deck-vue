<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import api from "../services/api";

const route = useRoute();
const heroId = route.params.id;
const hero = ref({});
const loading = ref(true);

const getHeroById = async () => {
  const response = await api.get(`/${heroId}`);
  hero.value = response.data;
  loading.value = false;
};

onMounted(() => {
  getHeroById();
});
</script>

<template>
  <div v-if="loading" class="loading">Loading...</div>
  <div v-else class="card-hero">
    <h3>{{ hero.name }}</h3>
    <img :src="hero.image.url ? hero.image.url : ''" alt="" />
  </div>
</template>

