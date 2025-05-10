<template>
  <div class="mt-auto flex flex-col items-start gap-y-12" :key="game.id">
    <Motion as="h1"
      :initial="{ opacity: 0, y: 20 }"
      :animate="{ opacity: 1, y: 0 }"
      :transition="{ type: 'spring', stiffness: 250, damping: 25, delay: 0.1 }"
      class="text-3xl @md:text-5xl @lg:text-6xl xl:text-5xl font-bold mb-4 text-shadow"
    >
      <NuxtImg v-if="game.logo" :src="game.logo" :alt="game.name" class="max-h-48 object-contain" />
      <template v-else>{{ game.name }}</template>
    </Motion>
    <Motion as="p"
      :initial="{ opacity: 0, y: 20 }"
      :animate="{ opacity: 1, y: 0 }"
      :transition="{ type: 'spring', stiffness: 250, damping: 25, delay: 0.2 }"
      class="text-xl @md:text-2xl @lg:text-4xl xl:text-2xl mb-8 text-shadow"
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
        class="bg-white/15 hover:bg-white/15 text-white font-bold py-3 @md:py-5 @lg:py-6 xl:py-4 w-32 @md:w-44 @lg:w-sm xl:w-40 rounded-full text-lg @md:text-2xl @lg:text-3xl xl:text-xl"
      >
        Play Game
      </Motion>
      <Motion as="button"
        :whileHover="{ scale: 1.05 }"
        :whileTap="{ scale: 0.95 }"
        :transition="{ type: 'spring', stiffness: 400, damping: 15 }"
        class="bg-white/15 hover:bg-white/15 text-white font-bold p-3 @md:p-4 @lg:p-5 xl:p-3 rounded-full"
      >
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-8 h-8 @md:w-10 @md:h-10 @lg:w-12 @lg:h-12 xl:w-8 xl:h-8">
          <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM12.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM18.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0Z" />
        </svg>
      </Motion>
    </Motion>
  </div>
</template>

<script setup>
import { Motion } from 'motion-v';
import { NuxtImg } from '#components';

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