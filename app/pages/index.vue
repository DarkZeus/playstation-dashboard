<template>
  <div class="relative min-h-screen text-white">
    <div class="absolute top-0 left-0 w-full h-full bg-black -z-30 pointer-events-none" aria-hidden="true"></div>
    
    <!-- Animated Background Image Layers for Crossfade -->
    <Motion as="div"
      v-if="prevBackgroundCover && prevBackgroundCover !== selectedGame.backgroundCover"
      :key="prevBackgroundCover"
      :initial="{ opacity: 1 }"
      :animate="{ opacity: 0 }"
      :transition="{ duration: 0.7, ease: 'easeInOut' }"
      class="fixed inset-0 bg-black bg-cover bg-center -z-20 min-h-screen"
      :style="{ backgroundImage: `url(${prevBackgroundCover})` }"
      @motionend="onPrevBgFadeOut"
    >
      &nbsp;
    </Motion>
    <Motion as="div"
      :key="selectedGame.backgroundCover"
      :initial="{ opacity: 0 }"
      :animate="{ opacity: 1 }"
      :transition="{ duration: 0.7, ease: 'easeInOut' }"
      class="fixed inset-0 bg-black bg-cover bg-center -z-20 min-h-screen"
      :style="{ backgroundImage: `url(${selectedGame.backgroundCover})` }"
    >
      &nbsp;
    </Motion>
    <!-- Overlay Layer -->
    <div
      class="fixed inset-0 -z-10 pointer-events-none bg-gradient-to-r from-black/70 to-black/45"
    ></div>

    <!-- Foreground Content -->
    <div class="relative z-0 flex flex-col min-h-screen">
      <Navbar />
      <main class="relative z-10 flex flex-col justify-end flex-grow p-10 pb-20">
        <GameCarousel :games="games" :selectedGameIndex="selectedGameIndex" @select-game="selectGame" />
        <GameDetails :game="selectedGame" />
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';
import { Motion } from 'motion-v';
import Navbar from '../components/Navbar.vue';
import GameCarousel from '../components/GameCarousel.vue';
import GameDetails from '../components/GameDetails.vue';

const games = [
  { id: 1, name: "Cyberpunk 2077", description: "Become a mercenary in the living, breathing metropolis of Night City.", cover: 'https://gmedia.playstation.com/is/image/SIEPDC/Cyberpunk-2077-thumbnail-01-ps4-en-12nov20?$800px--t$', backgroundCover: 'https://gmedia.playstation.com/is/image/SIEPDC/cyberpunk-2077-screen-06-ps4-en-06jun19?$2400px$' },
  { id: 2, name: "Days Gone", description: "Ride into a desperate, dog-eat-dog world in the definitive Days Gone experience.", cover: 'https://images.igdb.com/igdb/image/upload/t_cover_big/co94bn.webp', backgroundCover: 'https://images.igdb.com/igdb/image/upload/t_original/r5mn9rt7aqvf5nrn8dqq.jpg' },
  { id: 3, name: "Death Stranding Director's Cut", description: "Connect a fractured society in this genre-defying open-world adventure.", cover: 'https://image.api.playstation.com/vulcan/ap/rnd/202106/2214/a8zjXIdTwKslJ2HvoJvY34a1.jpg?w=780', backgroundCover: 'https://gmedia.playstation.com/is/image/SIEPDC/death-stranding-directors-cut-screenshot-04-announce-en-01jul21?$2400px$'  },
];

const selectedGameIndex = ref(0);
const selectedGame = computed(() => games[selectedGameIndex.value]);

const prevBackgroundCover = ref(null);

watch(selectedGameIndex, (newIdx, oldIdx) => {
  if (games[oldIdx] && games[oldIdx].backgroundCover !== games[newIdx].backgroundCover) {
    prevBackgroundCover.value = games[oldIdx].backgroundCover;
  }
});

function onPrevBgFadeOut() {
  prevBackgroundCover.value = null;
}

function selectGame(index) {
  selectedGameIndex.value = index;
}
</script>

<style scoped>
.min-h-screen {
  min-height: 100dvh;
}
</style>