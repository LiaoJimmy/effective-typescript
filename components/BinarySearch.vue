<template>
  <div class="binary-search-container">
    <h2>Binary search visualization</h2>
    
    <div class="input-section">
      <div class="form-group">
        <label for="array-input">Enter a sorted array (comma separated numbers):</label>
        <input 
          id="array-input" 
          v-model="arrayInput" 
          @change="validateArray"
          placeholder="e.g. 1,3,5,7,9,11,13"
        />
        <div v-if="arrayError" class="error">{{ arrayError }}</div>
      </div>
      
      <div class="form-group">
        <label for="target-input">Enter a number to search for:</label>
        <input 
          id="target-input" 
          v-model="targetInput" 
          @change="validateTarget"
          placeholder="e.g. 9"
        />
        <div v-if="targetError" class="error">{{ targetError }}</div>
      </div>
      
      <button @click="startSearch" :disabled="!isValid || isSearching">Start Search</button>
      <button @click="resetSearch" :disabled="!isSearching && !hasSearched">Reset</button>
      <button @click="nextStep" :disabled="!isSearching || stepPromiseResolve === null">Next Step</button>
    </div>
    
    <div v-if="array.length > 0" class="visualization-section">
      <div class="array-container">
        <div 
          v-for="(item, index) in array" 
          :key="index"
          class="array-item"
          :class="{
            'low': index === low && isSearching,
            'high': index === high && isSearching,
            'mid': index === mid && isSearching,
            'current': index === low && low === high && found,
            'outside-range': (index < low || index > high) && isSearching
          }"
        >
          {{ item }}
        </div>
      </div>
      
      <div class="info-section" v-if="isSearching || hasSearched">
        <div v-if="isSearching || hasSearched">
          <p>Searching for: {{ target }}</p>
          <p v-if="isSearching">Current range: [{{ low }}, {{ high }}]</p>
          <p v-if="isSearching">Middle index: {{ mid }}, Middle value: {{ array[mid] }}</p>
          <p v-if="hasSearched && found">Found {{ target }} at index {{ resultIndex }}!</p>
          <p v-if="hasSearched && !found">{{ target }} not found in the array.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch, onMounted } from 'vue';

// Reactive state
const arrayInput = ref('1,3,5,7,9,11,13');
const targetInput = ref('9');
const array = ref([]);
const target = ref(null);
const low = ref(0);
const high = ref(0);
const mid = ref(0);
const isSearching = ref(false);
const hasSearched = ref(false);
const found = ref(false);
const resultIndex = ref(-1);
const searchSteps = ref([]);
const arrayError = ref('');
const targetError = ref('');
const stepPromiseResolve = ref(null); // To manage pausing for next step

onMounted(() => {
  validateArray();
  validateTarget();
});

const isValid = computed(() => {
  return array.value.length > 0 && target.value !== null && !arrayError.value && !targetError.value;
});

function validateArray() {
  try {
    if (!arrayInput.value.trim()) {
      arrayError.value = 'Please enter an array';
      array.value = [];
      return;
    }
    
    const parsed = arrayInput.value.split(',').map(item => {
      const num = Number(item.trim());
      if (isNaN(num)) throw new Error('Array must contain only numbers');
      return num;
    });
    
    // Check if sorted
    for (let i = 1; i < parsed.length; i++) {
      if (parsed[i] < parsed[i-1]) {
        arrayError.value = 'Array must be sorted in ascending order';
        return;
      }
    }
    
    arrayError.value = '';
    array.value = parsed;
  } catch (e) {
    arrayError.value = e.message;
    array.value = [];
  }
}

function validateTarget() {
  if (!targetInput.value.trim()) {
    targetError.value = 'Please enter a target number';
    target.value = null;
    return;
  }
  
  const num = Number(targetInput.value.trim());
  if (isNaN(num)) {
    targetError.value = 'Target must be a number';
    target.value = null;
    return;
  }
  
  targetError.value = '';
  target.value = num;
}

// Function to pause execution until nextStep is called
function pauseForNextStep() {
  return new Promise(resolve => {
    stepPromiseResolve.value = resolve;
  });
}

// Function called by the Next Step button
function nextStep() {
  if (stepPromiseResolve.value) {
    stepPromiseResolve.value();
    stepPromiseResolve.value = null; // Clear the resolver after use
  }
}

// Modify startSearch to initiate the step-by-step search
async function startSearch() {
  if (!isValid.value || isSearching.value) return;
  
  resetSearch(); // Reset previous state first
  isSearching.value = true;
  searchSteps.value = [];
  low.value = 0;
  high.value = array.value.length - 1;
  found.value = false;
  resultIndex.value = -1; // Ensure resultIndex is reset
  
  // Start the step-by-step search process
  binarySearchStepByStep(); 
}

// Modify resetSearch to handle potential pending steps
function resetSearch() {
  isSearching.value = false; // Stop any ongoing search loop
  if (stepPromiseResolve.value) {
    stepPromiseResolve.value(); // Resolve any pending pause
    stepPromiseResolve.value = null;
  }
  hasSearched.value = false;
  found.value = false;
  resultIndex.value = -1;
  searchSteps.value = [];
  // Reset low/high/mid only if array is present, otherwise validation handles it
  if (array.value.length > 0) {
      low.value = 0;
      high.value = array.value.length - 1;
      // Calculate initial mid for display before first step, or set to 0 if array is empty
      mid.value = array.value.length > 0 ? Math.floor((low.value + high.value) / 2) : 0; 
  } else {
      low.value = 0;
      high.value = 0;
      mid.value = 0;
  }
}

// Replace binarySearch with the step-by-step version
async function binarySearchStepByStep() {
  // Initial state before the first step - mid calculation moved to reset/start for immediate display
  // if (low.value <= high.value) {
  //    mid.value = Math.floor((low.value + high.value) / 2);
  // }

  while (low.value <= high.value) {
    if (!isSearching.value) return; // Check if reset was called

    mid.value = Math.floor((low.value + high.value) / 2);
    searchSteps.value.push(
      `Step ${searchSteps.value.length + 1}: Check index ${mid.value}. Value is ${array.value[mid.value]}. Comparing with target ${target.value}.`
    );
    
    // Pause and wait for the "Next Step" button click
    await pauseForNextStep();
    if (!isSearching.value) return; // Check if reset was called during pause

    const midValue = array.value[mid.value];

    if (midValue === target.value) {
      searchSteps.value.push(`Found ${target.value} at index ${mid.value}!`);
      found.value = true;
      resultIndex.value = mid.value;
      isSearching.value = false; // Search finished
      hasSearched.value = true;
      // Ensure the final state is shown without needing another click
      if (stepPromiseResolve.value) {
          stepPromiseResolve.value();
          stepPromiseResolve.value = null;
      }
      return; // Exit the loop and function
    } else if (midValue < target.value) {
      const nextLow = mid.value + 1;
      searchSteps.value.push(`Result: ${midValue} < ${target.value}. Discard left half. New range: [${nextLow}, ${high.value}]`);
      low.value = nextLow;
    } else { // midValue > target.value
      const nextHigh = mid.value - 1;
      searchSteps.value.push(`Result: ${midValue} > ${target.value}. Discard right half. New range: [${low.value}, ${nextHigh}]`);
      high.value = nextHigh;
    }

    // If the range becomes invalid, the loop condition (low <= high) will handle termination.
    // Pause again to show the result of the comparison and the new range before the next iteration's check
    await pauseForNextStep();
     if (!isSearching.value) return; // Check if reset was called during pause
  }

  // Target not found after the loop
  if (!found.value && isSearching.value) { // Ensure search wasn't reset
    searchSteps.value.push(`${target.value} not found in the array.`);
    isSearching.value = false; // Search finished
    hasSearched.value = true;
     // Ensure the final state is shown without needing another click
      if (stepPromiseResolve.value) {
          stepPromiseResolve.value();
          stepPromiseResolve.value = null;
      }
  }
}

// Remove the old async function binarySearch() { ... }
// It has been replaced by binarySearchStepByStep()

// ... existing code ...
</script>

<style scoped>
.binary-search-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  max-height: 80vh; /* Limit height to 80% of viewport height */
  overflow-y: auto; /* Add vertical scrollbar if content overflows */
}

.input-section {
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  margin-right: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

.error {
  color: red;
  font-size: 0.8em;
  margin-top: 5px;
}

.visualization-section {
  margin-top: 30px;
}

.array-container {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-bottom: 20px;
}

.array-item {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: #f9f9f9;
  transition: all 0.3s ease;
}

.low {
  border: 2px solid blue;
}

.high {
  border: 2px solid green;
}

.mid {
  background-color: #ffeb3b;
  border: 2px solid red;
  font-weight: bold;
}

.current {
  background-color: #4CAF50;
  color: white;
  font-weight: bold;
  transform: scale(1.1);
}

.outside-range {
  opacity: 0.3;
}

.info-section {
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #eee;
  border-radius: 4px;
  background-color: #f9f9f9;
}

.info-section p {
  margin: 5px 0;
}

.steps-container {
  border: 1px solid #eee;
  border-radius: 4px;
  padding: 10px;
  max-height: 200px;
  overflow-y: auto;
}

.step {
  margin-bottom: 5px;
  padding: 5px;
  border-bottom: 1px solid #eee;
}
</style>