<script setup lang="ts">
import type { Song } from '@/models/song.interface';
const props = defineProps<{ song: Song }>();
</script>

<template>
  <main>
    <div class="movie-item">
      <h3>{{ props.song.title }} ({{ props.song.artist }})</h3>
      <p>{{ props.song.artist }}</p>
      <p>{{ props.song.duration }}</p>
      <span class="movie-end-line">
        <p v-if="props.song.isTopHit" class="label-in-theaters">Top hit!</p>
      </span>
    </div>
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
