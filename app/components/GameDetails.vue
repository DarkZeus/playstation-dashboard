<template>
  <div class="mt-auto flex flex-col items-start gap-y-12" :key="game.id">
    <Motion as="h1"
      :initial="{ opacity: 0, y: 20 }"
      :animate="{ opacity: 1, y: 0 }"
      :transition="{ type: 'spring', stiffness: 250, damping: 25, delay: 0.1 }"
      class="text-6xl font-bold mb-4 text-shadow"
    >
      <img v-if="game.logo" :src="game.logo" :alt="game.name" class="max-h-48 object-contain" >
      <template v-else>{{ game.name }}</template>
    </Motion>
    <Motion as="p"
      :initial="{ opacity: 0, y: 20 }"
      :animate="{ opacity: 1, y: 0 }"
      :transition="{ type: 'spring', stiffness: 250, damping: 25, delay: 0.2 }"
      class="text-4xl mb-8  text-shadow"
    >
      {{ game.description }}
    </Motion>
    <Motion as="div"
      :initial="{ opacity: 0, y: 20 }"
      :animate="{ opacity: 1, y: 0 }"
      :transition="{ type: 'spring', stiffness: 250, damping: 25, delay: 0.3 }"
      class="flex items-center space-x-4"
    >
      <Motion as="button"
        :whileHover="{ scale: 1.05 }"
        :whileTap="{ scale: 0.95 }"
        :transition="{ type: 'spring', stiffness: 400, damping: 15 }"
        class="bg-white/15 hover:bg-white/15 text-white font-bold py-6 w-sm rounded-full text-3xl"
      >
        Play Game
      </Motion>
      <Motion as="button"
        :whileHover="{ scale: 1.05 }"
        :whileTap="{ scale: 0.95 }"
        :transition="{ type: 'spring', stiffness: 400, damping: 15 }"
        class="bg-white/15 hover:bg-white/15 text-white font-bold p-5 rounded-full"
      >
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-12 h-12">
          <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM12.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM18.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0Z" />
        </svg>
      </Motion>
    </Motion>
  </div>
</template>

<script setup>
import { Motion } from 'motion-v';

const props = defineProps({
  game: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
.text-shadow {
  text-shadow: 0px 0px 8px rgba(0, 0, 0, 0.7);
}
</style> 