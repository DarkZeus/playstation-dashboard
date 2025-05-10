<template>
  <div ref="carouselRef" class="mb-10 pb-4 px-4 @md:px-10 flex space-x-1 items-start overflow-x-auto">
    <Motion as="div"
      v-for="(game, index) in games"
      :key="game.id"
      :ref="el => { if (index === selectedGameIndex) selectedGameRef = el.$el || el }"
      @click="$emit('select-game', index)"
      :initial="{ opacity: index === selectedGameIndex ? 1 : 0.7 }"
      :animate="{ opacity: index === selectedGameIndex ? 1 : 0.7 }"
      :transition="{ type: 'spring', stiffness: 400, damping: 17 }"
      class="cursor-pointer relative "
    >
      <div
        :class="[
          index === selectedGameIndex
            ? 'w-32 h-32 p-1 @md:w-52 @md:h-52 @md:p-2 @lg:w-64 @lg:h-64 @lg:p-3 xl:w-48 xl:h-48 xl:p-2'
            : 'w-20 h-20 p-0.5 @md:w-32 @md:h-32 @md:p-1 @lg:w-40 @lg:h-40 @lg:p-2 xl:w-28 xl:h-28 xl:p-1',
          'aspect-square rounded-[25%] flex items-center justify-center transition-all overflow-hidden',
        ]"
      >
        <NuxtImg
          :src="game.cover"
          :alt="game.name"
          class="w-full h-full object-cover rounded-lg"
        />
        <Motion
          as="span"
          :initial="{ opacity: 0 }"
          :animate="{ opacity: 1 }"
          :transition="{ type: 'spring', stiffness: 400, damping: 17 }"
          v-if="index === selectedGameIndex"
          class="absolute left-full ml-2 @md:ml-3 bottom-2 @md:bottom-6 text-lg @md:text-2xl @lg:text-4xl xl:text-xl text-white transition-colors duration-300 size-max"
        >
          {{ game.name }}
        </Motion>
      </div>
      
    </Motion>
  </div>
</template>

<script setup>
import { Motion } from 'motion-v';
import { NuxtImg } from '#components';
import { ref, watch, nextTick, computed } from 'vue';

const carouselRef = ref(null);
const selectedGameRef = ref(null);

const props = defineProps({
  games: {
    type: Array,
    required: true
  },
  selectedGameIndex: {
    type: Number,
    required: true
  }
});


defineEmits(['select-game']);
</script>

<style scoped>
.overflow-x-auto::-webkit-scrollbar {
  height: 8px;
}

.overflow-x-auto::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
}

.overflow-x-auto::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.3);
  border-radius: 10px;
}

.overflow-x-auto::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.5);
}
</style> 