<template>
  <div class="mb-10 pb-4 flex space-x-6 items-start">
    <Motion as="div"
      v-for="(game, index) in games"
      :key="game.id"
      @click="$emit('select-game', index)"
      :whileTap="{ scale: 0.95 }"
      :initial="{ opacity: index === selectedGameIndex ? 1 : 0.7 }"
      :animate="{ opacity: index === selectedGameIndex ? 1 : 0.7 }"
      :transition="{ type: 'spring', stiffness: 400, damping: 17 }"
      class="cursor-pointer"
    >
      <div
        :class="[
          index === selectedGameIndex
            ? 'w-32 h-32 p-2'
            : 'w-20 h-20 p-1',
          'aspect-square rounded-xl flex items-center justify-center transition-all overflow-hidden',
          index === selectedGameIndex
            ? 'border-4 border-blue-500 bg-white/10 shadow-lg shadow-blue-400/40'
            : 'border-2 border-gray-500 bg-white/5'
        ]"
      >
        <img
          :src="game.cover"
          :alt="game.name"
          class="w-full h-full object-cover rounded-lg"
        />
      </div>
      <p
        v-if="index === selectedGameIndex"
        class="text-center text-sm mt-2 font-semibold text-white transition-colors duration-300"
      >
        {{ game.name }}
      </p>
    </Motion>
  </div>
</template>

<script setup>
import { Motion } from 'motion-v';

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
/* Custom scrollbar for webkit browsers for the carousel */
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