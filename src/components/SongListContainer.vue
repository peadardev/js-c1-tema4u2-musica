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
      <span class="number-songs">
        <span class="number-showing">
          <div class="showing-label">Mostrant:</div>
          <div class="showing-value">{{ songs.length }}</div>
        </span>
        <div class="number-total">Total: {{ numTotal }}</div>
      </span>
    </span>
    <div class="songs-list">
      <div class="songs-container" v-for="song of songs" :key="song.id">
        <SongItem v-if="isShowAll || song.isTopHit" :song="song" />
      </div>
    </div>
  </main>
</template>

<style scoped>
.container-control {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.number-songs {
  display: flex;
  align-items: center;
  padding: 1rem;
}
.number-showing {
  display: flex;
  align-items: center;
  padding: 1rem;
}
.showing-label {
  font-size: 14px;
  padding: 5px;
}
.showing-value {
  font-size: 24px;
  font-weight: bold;
  color: darkblue;
}
.number-total {
  font-size: 14px;
  background-color: whitesmoke;
  padding: 10px;
}
.button-toggle {
  height: 2.5rem;
  padding: 10px 20px;
  margin: 1rem;
  background: lightsteelblue;
  border-radius: 8px;
  cursor: pointer;
  border: 1px solid gray;
}
.songs-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 10px;
}
.songs-container {
  display: flex;
}
</style>
