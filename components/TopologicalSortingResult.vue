<script setup>
import { ref, computed } from 'vue'

// Layers based on topological sort
const layers = [
  {
    id: 1,
    nodes: [
      { id: 'A', name: 'layout.js' },
      { id: 'G', name: 'canvas.js' }
    ]
  },
  {
    id: 2,
    nodes: [
      { id: 'E', name: 'math.js' },
      { id: 'F', name: 'helper.js' },
      { id: 'B', name: 'utils.js' },
    ]
  },
  {
    id: 3,
    nodes: [
      { id: 'C', name: 'tickers.js' }
    ]
  }
]

const currentStep = ref(1)

// Get all node names up to the current step, starting from the deepest layer
const highlightedNodes = computed(() => {
  return layers
    .slice(layers.length - currentStep.value)
    .flatMap(l => l.nodes.map(n => n.name))
})

function nextStep() {
  if (currentStep.value < layers.length) {
    currentStep.value++
  }
}

function reset() {
  currentStep.value = 1
}
</script>

<template>
  <h1>Topological Sorting Result</h1>
  <div class="p-4 font-sans flex flex-col items-center">
    <div class="flex items-center mb-4">
      <button @click="nextStep" :disabled="currentStep >= layers.length" class="w-24 bg-blue-500 text-white text-sm font-bold py-2 px-4 rounded mr-2 disabled:bg-gray-400 disabled:cursor-not-allowed">
        Next
      </button>
      <button @click="reset" class="w-24 text-sm bg-pink-500 text-white font-bold py-2 px-4 rounded">
        Reset
      </button>
      <div class="text-center text-sm ml-4 w-24">
        Step: {{ currentStep }} / {{ layers.length }}
      </div>
    </div>

    <div class="relative w-full max-w-2xl h-84 border rounded-lg bg-gray-50 p-4">
      <!-- Visual representation of layers -->
      <div class="flex justify-around h-full">
        <!-- Layer 1 -->
        <div class="flex flex-col justify-around">
          <div v-for="node in layers[0].nodes" :key="node.id"
               class="p-3 rounded-lg text-center transition-colors duration-300 w-32"
               :class="highlightedNodes.includes(node.name) ? 'bg-teal-500 text-white' : 'bg-gray-300 text-gray-800'">
            {{ node.name }}
          </div>
        </div>

        <!-- Layer 2 -->
        <div class="flex flex-col justify-around">
          <div v-for="node in layers[1].nodes" :key="node.id"
               class="p-3 rounded-lg text-center transition-colors duration-300 w-32"
               :class="highlightedNodes.includes(node.name) ? 'bg-teal-500 text-white' : 'bg-gray-300 text-gray-800'">
            {{ node.name }}
          </div>
        </div>

        <!-- Layer 3 -->
        <div class="flex flex-col justify-center">
          <div v-for="node in layers[2].nodes" :key="node.id"
               class="p-3 rounded-lg text-center transition-colors duration-300 w-32"
               :class="highlightedNodes.includes(node.name) ? 'bg-teal-500 text-white' : 'bg-gray-300 text-gray-800'">
            {{ node.name }}
          </div>
        </div>
      </div>

      <!-- Arrows (simplified for clarity) -->
      <svg class="absolute top-0 left-0 w-full h-full" style="pointer-events: none;">
        <defs>
          <marker id="arrowhead-vue" markerWidth="4.5" markerHeight="5.25" refX="3" refY="2.625" orient="auto" class="fill-current text-black-400">
            <polygon points="0 0, 4.5 2.625, 0 5.25" />
          </marker>
        </defs>
        <!-- A -> B -->
        <line x1="30%" y1="27.5%" x2="40%" y2="75%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-vue)" />
        <!-- B -> C -->
        <line x1="60%" y1="75%" x2="70%" y2="50%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-vue)" />
        <!-- A -> E -->
        <line x1="30%" y1="27.5%" x2="40%" y2="22.5%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-vue)" />
        <!-- A -> F -->
        <line x1="30%" y1="27.5%" x2="40%" y2="50%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-vue)" />
        <!-- G -> B -->
        <line x1="30%" y1="77%" x2="40%" y2="77%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-vue)" />
      </svg>
    </div>
  </div>
</template>
