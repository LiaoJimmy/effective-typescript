<script setup>
import { ref, computed } from 'vue'

const graph = {
  'layout': ['utils', 'math', 'helper'],
  'canvas': ['utils'],
  'utils': ['tickers'],
  'tickers': [],
  'math': [],
  'helper': [],
};
const allNodes = Object.keys(graph);

const nodePositions = {
  'layout': { top: '50%', left: '5%' },
  'canvas': { top: '70%', left: '5%' },
  'utils': { top: '50%', left: '38%' },
  'tickers': { top: '50%', left: '70%' },
  'math': { top: '30%', left: '38%' },
  'helper': { top: '70%', left: '38%' },
};

const steps = [];
let permanent = new Set();
let temporary = new Set();
let result = [];
let cycleDetected = false;

function generateSteps() {
  // Reset state
  steps.length = 0;
  permanent = new Set();
  temporary = new Set();
  result = [];
  cycleDetected = false;

  steps.push({
    permanent: new Set(),
    temporary: new Set(),
    result: [],
    message: 'Start: Initialize sets and result list.',
    currentNode: null,
  });

  function visit(node) {
    if (cycleDetected) return;

    steps.push({
      permanent: new Set(permanent),
      temporary: new Set(temporary),
      result: [...result],
      message: `Visiting '${node}'...`,
      currentNode: node,
    });

    if (permanent.has(node)) {
      steps.push({
        permanent: new Set(permanent),
        temporary: new Set(temporary),
        result: [...result],
        message: `'${node}' is already permanent. Skipping.`,
        currentNode: node,
      });
      return;
    }
    if (temporary.has(node)) {
      cycleDetected = true;
      steps.push({
        permanent: new Set(permanent),
        temporary: new Set(temporary),
        result: [...result],
        message: `Cycle detected at '${node}'! It's in the temporary set.`,
        currentNode: node,
      });
      return;
    }

    temporary.add(node);
    steps.push({
      permanent: new Set(permanent),
      temporary: new Set(temporary),
      result: [...result],
      message: `Added '${node}' to temporary set.`,
      currentNode: node,
    });

    const children = graph[node] || [];
    for (const child of children) {
      visit(child);
      if (cycleDetected) return;
    }

    temporary.delete(node);
    permanent.add(node);
    result.push(node);
    steps.push({
      permanent: new Set(permanent),
      temporary: new Set(temporary),
      result: [...result],
      message: `Finished with '${node}'. Moved to permanent set and added to result.`,
      currentNode: node,
    });
  }

  for (const vertex of allNodes) {
    if (!permanent.has(vertex)) {
      visit(vertex);
      if (cycleDetected) break;
    }
  }

  steps.push({
    permanent: new Set(permanent),
    temporary: new Set(temporary),
    result: [...result],
    message: cycleDetected ? 'Algorithm halted due to cycle.' : 'Topological sort complete!',
    currentNode: null,
  });
}

generateSteps();

const currentStep = ref(0);

const currentDisplayState = computed(() => {
  return steps[currentStep.value];
});

function nextStep() {
  if (currentStep.value < steps.length - 1) {
    currentStep.value++;
  }
}

function prevStep() {
  if (currentStep.value > 0) {
    currentStep.value--;
  }
}

function reset() {
  currentStep.value = 0;
}

function getNodeClass(node) {
  const state = currentDisplayState.value;
  if (state.currentNode === node) {
    return 'bg-yellow-400';
  }
  if (state.permanent.has(node)) {
    return 'bg-green-500 text-white';
  }
  if (state.temporary.has(node)) {
    return 'bg-blue-500 text-white';
  }
  return 'bg-gray-300 text-gray-800';
}
</script>

<template>
  <div class="font-sans flex flex-col items-center">
    <!-- Controls -->
    <div class="flex items-center mt-2 mb-2">
      <button @click="prevStep" :disabled="currentStep === 0" class="w-24 bg-gray-500 text-white text-sm font-bold py-2 px-4 rounded mr-2 disabled:bg-gray-400 disabled:cursor-not-allowed">
        Previous
      </button>
      <button @click="nextStep" :disabled="currentStep >= steps.length - 1" class="w-24 bg-blue-500 text-white text-sm font-bold py-2 px-4 rounded mr-2 disabled:bg-gray-400 disabled:cursor-not-allowed">
        Next
      </button>
      <button @click="reset" class="w-24 text-sm bg-pink-500 text-white font-bold py-2 px-4 rounded">
        Reset
      </button>
      <div class="text-center text-sm ml-4">
        Step: {{ currentStep + 1 }} / {{ steps.length }}
      </div>
    </div>

    <!-- Main Content -->
    <div class="w-full max-w-4xl flex space-x-4 mt-2">
      <!-- Graph Visualization -->
      <div class="w-2/3 border rounded-lg p-4 relative h-112">
        <h3 class="text-lg font-bold mb-2 text-center">Graph Nodes</h3>
        
        <!-- Nodes -->
        <div v-for="node in allNodes" :key="node"
             class="absolute p-2 rounded-lg text-center transition-colors duration-300 w-20 text-sm"
             :class="getNodeClass(node)"
             :style="{ top: nodePositions[node].top, left: nodePositions[node].left }">
          {{ node }}.js
        </div>

        <!-- Arrows -->
        <svg class="absolute top-0 left-0 w-full h-full" style="pointer-events: none;">
          <defs>
            <marker id="arrowhead-topo" markerWidth="4.5" markerHeight="5.25" refX="3" refY="2.625" orient="auto" class="fill-current text-black-400">
              <polygon points="0 0, 4.5 2.625, 0 5.25" />
            </marker>
          </defs>
          <!-- layout -> utils -->
          <line x1="72%" y1="21%" x2="52%" y2="44%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-topo)" />
          <!-- layout -> math -->
          <line x1="70%" y1="21%" x2="25%" y2="21%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-topo)" />
          <!-- layout -> helper -->
          <line x1="70%" y1="21%" x2="25%" y2="71%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-topo)" />
          <!-- canvas -> utils -->
          <line x1="72%" y1="71%" x2="52%" y2="46%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-topo)" />
          <!-- utils -> tickers -->
          <line x1="40%" y1="46%" x2="25%" y2="46%" stroke="currentColor" class="text-black-400" stroke-width="1.5" marker-end="url(#arrowhead-topo)" />
        </svg>
      </div>

      <!-- Sets Display -->
      <div class="w-1/3 flex flex-col space-y-4">
        <!-- Temporary Set -->
        <div class="border rounded-lg p-4 flex-1">
          <h5 class="text-lg font-bold mb-2">Temporary</h5>
          <div class="flex flex-wrap gap-2 min-h-[2.5rem]">
            <span v-for="node in Array.from(currentDisplayState.temporary)" :key="node"
                  class="px-2 py-1 bg-blue-500 text-white rounded-full text-xs h-1.5rem">
              {{ node }}
            </span>
            <span v-if="currentDisplayState.temporary.size === 0" class="text-sm text-gray-500 italic">Empty</span>
          </div>
        </div>

        <!-- Permanent Set -->
        <div class="border rounded-lg p-4 flex-1">
          <h5 class="text-lg font-bold mb-2">Permanent</h5>
          <div class="flex flex-wrap gap-2 min-h-[2.5rem]">
            <span v-for="node in Array.from(currentDisplayState.permanent)" :key="node"
                  class="px-2 py-1 bg-green-500 text-white rounded-full text-xs h-1.5rem">
              {{ node }}
            </span>
             <span v-if="currentDisplayState.permanent.size === 0" class="text-gray-500 italic">Empty</span>
          </div>
        </div>

        <!-- Result List -->
        <div class="border rounded-lg p-4 flex-1">
          <h5 class="text-lg font-bold mb-2">Result</h5>
          <div class="flex flex-wrap gap-2 min-h-[2.5rem]">
            <span v-for="node in currentDisplayState.result" :key="node"
                  class="px-2 py-1 bg-purple-500 text-white rounded-full text-xs h-1.5rem">
              {{ node }}
            </span>
             <span v-if="currentDisplayState.result.length === 0" class="text-gray-500 italic">Empty</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
