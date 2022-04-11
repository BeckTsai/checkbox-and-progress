<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref, reactive } from 'vue';
import Checkbox from './components/Checkbox.vue'
import ProgessCircle from './components/ProgessCircle.vue'

const left = ref(false);
const right = ref(false);
const red = ref(false);
const blue = ref(false);
const green = ref(false);

const array = reactive([false, false, false])

const progressValue = ref(1);
const maxValue = ref(100);
const minValue = ref(0);

const circleValue = ref(6);
const progessClrcleValue = ref(94);

</script>

<template>
  <div class="flex items-center">
    <Checkbox v-model="right" label="Label on Right" direction="right"  />
    <span class="mx-4">This model data: {{ right }}</span>
  </div>
  <div class="flex items-center">
    <Checkbox v-model="left" label="Label on Left" direction="left"  />
    <span class="mx-4">This model data: {{ left }}</span>
  </div>
    <Checkbox v-model="red" label="red" color="red"  />
    <Checkbox v-model="blue" label="blue" color="blue"/>
    <Checkbox v-model="green" label="green" color="green"  />
  <div>
    <Checkbox v-for="(item, index) in array" :key="index" v-model="array[index]" label="green" color="green"  />
    {{ array }}
  </div>
  <div class="mb-4">
    <input type="number" v-model="progressValue" :max="maxValue" :min="minValue" class="mb-4 border-2 border-solid" />
    <ProgessCircle :value="progressValue" size="36" strokeWidth="10" :maxValue="maxValue" :minValue="minValue" fill="#000" />
    <ProgessCircle :value="progressValue" size="36" strokeWidth="18" :maxValue="maxValue" :minValue="minValue" />
    <ProgessCircle :value="progressValue" size="36" strokeWidth="7" :rotate="180" :maxValue="maxValue" :minValue="minValue" />
  </div>
  <div>
    <input type="number" v-model="circleValue" :max="95" :min="5" class="mb-4 border-2 border-solid" />
    <ProgessCircle :value="circleValue" size="36" strokeWidth="10" :maxValue="maxValue" :minValue="5" fill="#000" ringColor="#a3a3a3" />
    <input type="number" v-model="progessClrcleValue" :max="95" :min="5" class="mb-4 border-2 border-solid" />
    <ProgessCircle :value="progessClrcleValue" size="36" strokeWidth="18" :maxValue="95" :minValue="5" />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
