<script setup>
import { ref, computed } from 'vue'

// Graph structure for visualization
const columns = [
  {
    id: 1,
    nodes: [
      { id: 'A', name: 'layout.js' },
    ]
  },
  {
    id: 2,
    nodes: [
      { id: 'B', name: 'utils.js' },
      { id: 'E', name: 'math.js' },
      { id: 'F', name: 'helper.js' },
    ]
  },
  {
    id: 3,
    nodes: [
      { id: 'C', name: 'tickers.js' }
    ]
  }
]

// DFS traversal completion steps
const steps = [
  [],
  ['layout.js'],
  ['layout.js', 'utils.js'],
  ['layout.js', 'utils.js', 'tickers.js'],
  ['layout.js', 'utils.js', 'tickers.js', 'math.js'],
  ['layout.js', 'utils.js', 'tickers.js', 'math.js', 'helper.js'],
];

const currentStep = ref(0)

const completedNodes = computed(() => steps[currentStep.value]);

function nextStep() {
  if (currentStep.value < steps.length - 1) {
    currentStep.value++
  }
}

function reset() {
  currentStep.value = 0
}

function getNodeClass(nodeName) {
  if (completedNodes.value.includes(nodeName)) {
    return 'bg-teal-500 text-white'; // Visited (green)
  }
  return 'bg-gray-300 text-gray-800'; // Not visited (gray)
}
</script>

<template>
  <h1>DFS Result</h1>
  <div class="p-4 font-sans flex flex-col items-center">
    <div class="flex items-center mb-4">
      <button @click="nextStep" :disabled="currentStep >= steps.length - 1" class="w-24 bg-blue-500 text-white text-sm font-bold py-2 px-4 rounded mr-2 disabled:bg-gray-400 disabled:cursor-not-allowed">
        Next
      </button>
      <button @click="reset" class="w-24 text-sm bg-pink-500 text-white font-bold py-2 px-4 rounded">
        Reset
      </button>
      <div class="text-center text-sm ml-4 w-24">
        Step: {{ currentStep }} / {{ steps.length - 1 }}
      </div>
    </div>

    <div class="relative w-full max-w-2xl h-84 border rounded-lg bg-gray-50 p-4">
      <!-- Visual representation of layers -->
      <div class="flex justify-around h-full">
        <!-- Column 1 -->
        <div class="flex flex-col justify-center">
          <div v-for="node in columns[0].nodes" :key="node.id"
               class="p-3 rounded-lg text-center transition-colors duration-300 w-32"
               :class="getNodeClass(node.name)">
            {{ node.name }}
          </div>
        </div>

        <!-- Column 2 -->
        <div class="flex flex-col justify-around">
          <div v-for="node in columns[1].nodes" :key="node.id"
               class="p-3 rounded-lg text-center transition-colors duration-300 w-32"
               :class="getNodeClass(node.name)">
            {{ node.name }}
          </div>
        </div>

        <!-- Column 3 -->
        <div class="flex flex-col justify-center">
          <div v-for="node in columns[2].nodes" :key="node.id"
               class="p-3 rounded-lg text-center transition-colors duration-300 w-32"
               :class="getNodeClass(node.name)">
            {{ node.name }}
          </div>
        </div>
      </div>

      <!-- Arrows -->
      <svg class="absolute top-0 left-0 w-full h-full" style="pointer-events: none;">
        <defs>
          <marker id="arrowhead-dfs" markerWidth="4.5" markerHeight="5.25" refX="3" refY="2.625" orient="auto" class="fill-current text-black-400">
            <polygon points="0 0, 4.5 2.625, 0 5.25" />
          </marker>
        </defs>
        <!-- A -> B -->
        <line x1="28%" y1="50%" x2="42%" y2="25%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-dfs)" />
        <!-- B -> C -->
        <line x1="60%" y1="25%" x2="72%" y2="50%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-dfs)" />
        <!-- A -> E -->
        <line x1="28%" y1="50%" x2="42%" y2="50%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-dfs)" />
        <!-- A -> F -->
        <line x1="28%" y1="50%" x2="42%" y2="75%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-dfs)" />
      </svg>
    </div>
  </div>
</template>
