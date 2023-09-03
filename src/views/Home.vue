<script setup>
import api from "../services/api";
import { onMounted, ref, computed } from "vue";
import { useRouter } from 'vue-router';

const heroes = ref([]);
const loading = ref(true);
const search = ref("");

const router = useRouter();

async function getHero() {
  const selectedHeroIds = [
    "569",
    "508",
    "489",
    "17",
    "30",
    "31",
    "35",
    "34",
    "38",
    "60",
    "63",
    "64",
    "65",
    "66",
    "67",
    "68",
    "69",
    "70",
    "71",
    "73",
    "95",
    "106",
    "107",
    "108",
    "149",
    "156",
    "160",
    "161",
    "165",
    "196",
    "194",
    "226",
    "225",
    "233",
    "263",
    "265",
    "266",
    "267",
    "275",
    "278",
    "280",
    "282",
    "283",
    "303",
    "308",
    "307",
    "309",
    "310",
    "313",
    "314",
    "315",
    "316",
    "317",
    "318",
    "332",
    "346",
    "370",
    "394",
    "405",
    "414",
    "416",
    "418",
    "427",
    "444",
    "476",
    "480",
    "485",
    "490",
    "527",
    "561",
    "589",
    "618",
    "619",
    "620",
    "621",
    "622",
    "623",
    "624",
    "625",
    "638",
    "637",
    "643",
    "644",
    "654",
    "655",
    "659",
    "660",
    "680",
    "687",
    "688",
    "689",
    "698",
    "697",
    "703",
    "714",
    "717",
    "718",
    "719",
    "720",
    "724",
    "730",
  ];

  const heroesData = await Promise.all(
    selectedHeroIds.map(async (heroId) => {
      const hero = await api.get(heroId);
      return hero.data;
    })
  );
  heroes.value = heroesData;
  loading.value = false;
}

onMounted(() => {
  getHero();
})

function detailsPage(hero) {
  router.push({ name: 'details', params: { id: hero } });
}

const filteredHeroes = computed(() => {
  if(heroes.value && search.value) {
    return heroes.value.filter((hero) => {
      return hero.name.toLowerCase().includes(search.value);
    })
  }
  return heroes.value;
})
</script>

<template>
  <div v-if="loading" class="loading">Loading...</div>
  <div v-else class="home">
    <input type="text" v-model="search" placeholder="Search a hero..." class="filter">
    <main class="container">
      <div class="card-hero" v-for="hero in filteredHeroes" :key="hero.id">
        <h3>{{ hero.name }}</h3>
        <img :src="hero.image.url ? hero.image.url : 'No image'" alt="" />
        <button @click="detailsPage(hero.id)">Details</button>
      </div>
    </main>
  </div>
</template>

<style>

body {
  background-color: #4c0edf;
}

.filter {
  padding: 1rem;
  width: 100%;
  border-radius: 5px;
  border: none;
  font-size: 1rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.loading {
  text-align: center;
  color: white;
  font-size: 2rem;
  font-weight: bold;
  padding: 1rem;

}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
}
.card-hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  margin: 1rem;
  border: 2px solid #4c0edf;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  width: 300px;
}

img {
  width: 100%;
}

button {
  background-color: gold;
  color: #4c0edf;
  padding: 0.5rem;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 1rem;
  font-weight: bold;
  width: 100%;
  margin-top: 1rem;
}

button:hover {
  background-color: #4c0edf;
  color: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  opacity: 0.8;
  cursor: pointer;
}
</style>