<template>
  <div ref="carouselRef" class="mb-10 pb-4 px-10 flex space-x-1 items-start overflow-x-auto">
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
            ? 'w-64 h-64 p-1'
            : 'w-40 h-40 p-0.5',
          'aspect-square rounded-[25%] flex items-center justify-center transition-all overflow-hidden',
        ]"
      >
        <img
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
          class="absolute left-full ml-3 bottom-6 text-4xl text-white transition-colors duration-300 size-max"
        >
          {{ game.name }}
        </Motion>
      </div>
      
    </Motion>
  </div>
</template>

<script setup>
import { Motion } from 'motion-v';
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