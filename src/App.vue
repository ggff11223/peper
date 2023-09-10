<script setup>
import { ref } from 'vue'

const random = ['ค้อน', 'กระดาษ', 'กรรไกร', 'ความรัก'];
const botRandom = ref('');
const playerRandom = ref('');
const botScore = ref(0);
const playerScore = ref(0);

function RandomImg(pic) {
  const allImgs = {
    'ค้อน': 'url',
    'กระดาษ':'url',
    'กรรไกร': 'url',
    'ความรัก': 'url',
  };

  return allImgs[pic];
}

function playButton() {
  botRandom.value = random[Math.floor(Math.random() * random.length)];
  playerRandom.value = random[Math.floor(Math.random() * random.length)];

  if (
    (botRandom.value === 'ค้อน' && playerRandom.value === 'กรรไกร') ||
    (botRandom.value === 'กระดาษ' && playerRandom.value === 'ค้อน') ||
    (botRandom.value === 'กรรไกร' && playerRandom.value === 'กระดาษ') ||
    (botRandom.value === 'ความรัก' && playerRandom.value === 'กรรไกร') ||
    (botRandom.value === 'ความรัก' && playerRandom.value === 'ค้อน') ||
    (botRandom.value === 'ความรัก' && playerRandom.value === 'กระดาษ')
  ) {
    botScore.value++;
  } else {
    playerScore.value++;
  }
}

function resetGame() {
  botRandom.value = '';
  playerRandom.value = '';
  botScore.value = 0;
  playerScore.value = 0;
}
</script>

<template>

    <div class="box-1">
      <h2 style="color: rgb(30, 255, 0);">Bot</h2>

      <img class="size-img" :src="RandomImg(botRandom)" /><br>
      {{ botRandom }}
    </div>
    <div class="box-2">
      <h2 style="color: rgb(69, 202, 255);">Player</h2>

      <img class="size-img" :src="RandomImg(playerRandom)"  /><br>
      {{ playerRandom }}
    </div>

  <div class="text-score">
    <p style="color: rgb(26, 255, 0);">Point of Bot : &nbsp; {{ botScore }}</p>
    <p style="color: rgb(69, 202, 255);"> Point of Player : &nbsp; {{ playerScore }}</p>
  </div>
  <button  @click="playButton" style="background-color: rgb(119, 198, 0);">Play</button> &nbsp;
  <button  @click="resetGame" style="background-color: red;">Reset</button>
</template>