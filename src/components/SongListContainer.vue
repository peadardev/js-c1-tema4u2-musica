<script setup lang="ts">
import type { Song } from '@/models/song.interface';
import SongItem from './SongItem.vue';
import musicImported from '@/data/songs.json';
import { ref, computed } from 'vue';

const isShowAll = ref(true);
const numTotal = ref(musicImported.length);
const textButton = computed(() => (isShowAll.value ? 'Mostra top hits' : 'Mostra tot'));
const songs = computed<Song[]>(() =>
  musicImported.filter((song) => isShowAll.value || song.isTopHit)
);
const toggleView = () => (isShowAll.value = !isShowAll.value);
</script>

<template>
  <main>
    <span class="container-control">
      <button @click="toggleView" class="button-toggle">
        {{ textButton }}
      </button>
      <div class="number-movies">Mostrant {{ songs.length }} cançons (total: {{ numTotal }})</div>
    </span>
    <span class="movies-list">
      <div class="movie-container" v-for="song of songs" :key="song.id">
        <SongItem v-if="isShowAll || song.isTopHit" :song="song" />
      </div>
    </span>
  </main>
</template>

<style scoped>
.container-control {
  display: flex;
  justify-content: space-between;
}
.number-movies {
  font-family: Arial, sans-serif;
  font-weight: bold;
  padding: 1rem;
}
img {
  max-width: 100px;
  width: 100%;
  height: auto;
}
.button-toggle {
  padding: 10px 20px;
  margin: 1rem;
  background: lightsteelblue;
  border-radius: 8px;
  cursor: pointer;
  border: 1px solid gray;
}
.movies-list {
  display: flex;
}

.movie-container {
  display: flex;
}
.movie-item {
  max-width: 260px;
  min-width: 200px;
  margin: 20px;
  background: black;
  border: 0px solid black;
  padding: 5px;
  margin: 5px;
  text-align: left;
  background-color: lightyellow;
}
.movie-end-line {
  display: flex;
  justify-content: space-between;
  font-style: italic;
}
.label-in-theaters {
  font-size: 12px;
  font-style: normal;
  color: yellow;
  background: green;
  padding: 8px;
  border-radius: 4px;
}
</style>
