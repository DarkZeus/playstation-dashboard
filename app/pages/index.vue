<template>
  <div class="relative min-h-screen text-white">
    <div v-if="showResolutionWarning" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80">
      <div class="bg-black/90 p-8 rounded-xl shadow-lg text-center max-w-md mx-auto">
        <h2 class="text-2xl font-bold mb-4">Screen Too Small</h2>
        <p class="text-lg">This dashboard is best viewed on screens at least 1280x720 pixels.<br />Please use a larger window or device.</p>
      </div>
    </div>
    <div class="absolute top-0 left-0 w-full h-full bg-black -z-30 pointer-events-none" aria-hidden="true"></div>
    
    <!-- Animated Background Image Layers for Crossfade -->
    <Motion as="div"
      v-if="prevBackgroundCover && prevBackgroundCover !== selectedGame?.backgroundCover"
      :key="prevBackgroundCover"
      :initial="{ opacity: 1 }"
      :animate="{ opacity: 0 }"
      :transition="{ duration: 0.7, ease: 'easeInOut' }"
      class="fixed inset-0 -z-20 min-h-screen overflow-hidden"
      @motionend="onPrevBgFadeOut"
    >
      <NuxtImg 
        :src="prevBackgroundCover"
        class="absolute inset-0 w-full h-full object-cover"
        alt=""
        loading="eager"
        decoding="async"
        fetchpriority="high"
        :width="1920"
        :height="1080"
      />
    </Motion>
    <Motion as="div"
      :key="selectedGame?.backgroundCover"
      :initial="{ opacity: 0 }"
      :animate="{ opacity: 1 }"
      :transition="{ duration: 0.7, ease: 'easeInOut' }"
      class="fixed inset-0 -z-20 min-h-screen overflow-hidden"
    >
      <NuxtImg 
        :src="selectedGame?.backgroundCover"
        class="absolute inset-0 w-full h-full object-cover"
        alt=""
        loading="eager"
        decoding="async"
        fetchpriority="high"
        :width="1920"
        :height="1080"
      />
    </Motion>
    <!-- Overlay Layer -->
    <div
      class="fixed inset-0 -z-10 pointer-events-none bg-gradient-to-r from-black/70 to-black/45"
    ></div>

    <!-- Foreground Content -->
    <div class="relative z-0 flex flex-col min-h-screen @container">
      <Navbar />
      <main class="relative z-10 flex flex-col justify-end flex-grow pb-20">
        <GameCarousel :games="games" :selectedGameIndex="selectedGameIndex" @select-game="selectGame" />
        <GameDetails :game="selectedGame" class="px-36" />
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue';
import { Motion } from 'motion-v';
import { NuxtImg } from '#components';
import Navbar from '../components/Navbar.vue';
import GameCarousel from '../components/GameCarousel.vue';
import GameDetails from '../components/GameDetails.vue';

const games = [
  {
    id: 1,
    name: "Cyberpunk 2077",
    description: "Become a mercenary in the living, breathing metropolis of Night City.",
    cover: 'https://gmedia.playstation.com/is/image/SIEPDC/Cyberpunk-2077-thumbnail-01-ps4-en-12nov20?$800px--t$',
    backgroundCover: 'https://gmedia.playstation.com/is/image/SIEPDC/cyberpunk-2077-screen-06-ps4-en-06jun19?$2400px$',
    logo: 'https://www.cyberpunk.net/build/images/home8/logo-cp77-yellow-en@1x-d74d8679.png'
  },
  {
    id: 2,
    name: "Days Gone",
    description: "Ride into a desperate, dog-eat-dog world in the definitive Days Gone experience.",
    cover: 'https://images.igdb.com/igdb/image/upload/t_cover_big/co94bn.webp',
    backgroundCover: 'https://images.igdb.com/igdb/image/upload/t_original/r5mn9rt7aqvf5nrn8dqq.jpg'
  },
  {
    id: 3, 
    name: "Death Stranding Director's Cut", 
    description: "Connect a fractured society in this genre-defying open-world adventure.", 
    cover: 'https://image.api.playstation.com/vulcan/ap/rnd/202106/2214/a8zjXIdTwKslJ2HvoJvY34a1.jpg?w=780', 
    backgroundCover: 'https://gmedia.playstation.com/is/image/SIEPDC/death-stranding-directors-cut-screenshot-04-announce-en-01jul21?$2400px$'
  },
];

const selectedGameIndex = ref(0);
const selectedGame = computed(() => games[selectedGameIndex.value]);

const prevBackgroundCover = ref(null);

watch(selectedGameIndex, (newIdx, oldIdx) => {
  if (games[oldIdx] && games[oldIdx]?.backgroundCover !== games[newIdx]?.backgroundCover) {
    prevBackgroundCover.value = games[oldIdx].backgroundCover;
  }
});

function onPrevBgFadeOut() {
  prevBackgroundCover.value = null;
}

function selectGame(index) {
  selectedGameIndex.value = index;
}

const minWidth = 1280;
const minHeight = 720;
const showResolutionWarning = ref(false);

function checkResolution() {
  showResolutionWarning.value = window.innerWidth < minWidth || window.innerHeight < minHeight;
}

onMounted(() => {
  checkResolution();
  window.addEventListener('resize', checkResolution);
});
onBeforeUnmount(() => {
  window.removeEventListener('resize', checkResolution);
});
</script>

<style scoped>
.min-h-screen {
  min-height: 100dvh;
}
</style>