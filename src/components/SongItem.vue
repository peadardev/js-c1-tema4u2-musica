<script setup lang="ts">
import type { Song } from '@/models/song.interface';
import { computed } from 'vue';
const props = defineProps<{ song: Song }>();
const labelTitle = computed<string>(() => (props.song.isTopHit ? '🔥' : ''));
const labelBottom = computed<string>(() => (props.song.isTopHit ? 'Top hit!' : '🎵'));
</script>

<template>
  <main class="song-item-ordinary" :class="{ 'song-item-hit': props.song.isTopHit }">
    <span class="song-title">
      <p class="song-name">{{ props.song.title }}</p>
      <p>{{ labelTitle }}</p>
    </span>
    <span class="song-artist">
      <em>Artista:</em>
      <p>{{ props.song.artist }}</p>
    </span>
    <span class="song-duration">
      <em>Duració:</em>
      <p>{{ props.song.duration }}</p>
    </span>
    <span class="song-label">
      <p class="label-ordinary" :class="{ 'label-top-hit': props.song.isTopHit }">
        {{ labelBottom }}
      </p>
    </span>
  </main>
</template>

<style scoped>
.song-item-ordinary {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 250px;
  height: 190px;
  font-family: Arial, sans-serif;
  font-size: 14px;
  margin: 20px;
  border: 1px solid lightgray;
  border-radius: 10px;
  padding: 10px;
  margin: 5px;
  text-align: left;
  background-color: lightyellow;
}
.song-item-hit {
  border: 2px solid orangered;
  background-color: lemonchiffon;
}
.song-title,
.song-artist,
.song-duration {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.song-name {
  font-size: 16px;
  font-weight: bold;
}
.song-label {
  display: flex;
  justify-content: center;
}
.label-ordinary {
  font-size: 12px;
  font-style: normal;
  color: black;
  background: whitesmoke;
  width: 60px;
  text-align: center;
  padding: 8px;
  border-radius: 15px;
}
.label-top-hit {
  color: yellow;
  background: orangered;
}
</style>
