<script setup>
import { ref,computed, getCurrentInstance } from 'vue'

const props = defineProps({
  label: String,
  color: {
    type: String,
    default: '#1866c1',
  },
  direction: {
    type: String,
    default: 'left',
  },
  modelValue: Boolean,
})

const emits = defineEmits(['update:modelValue'])

const uid = getCurrentInstance().uid;

const directionClass = computed(() => props.direction === 'left' ? 'flex-row' : 'flex-row-reverse');

const checkedStyle = computed(() => props.modelValue ? { 'background-color': props.color } : '')


</script>

<template>
  <label :for="`checkbox-${uid}`" :class="`inline-flex items-center ${directionClass}`">
    <div class="checkbox mx-2" :class="{ checked: props.modelValue }" :style="checkedStyle">
      <input :value="props.modelValue" type="checkbox" name="" :id="`checkbox-${uid}`" @change="emits('update:modelValue',$event.target.checked)">
      <span class="checked-icon" />
    </div>
    <span>{{label}}</span>
  </label>

</template>

<style lang="scss" scoped>
.checkbox {
  position: relative;
  width: 13px;
  height: 13px;
  border: 1px solid #aaa;
  border-radius: 3px;
  user-select: none;
}

.checked-icon {
  display: none;
  position: absolute;
  top: 2px;
  left: 1px;
  width: 10px;
  height: 10px;
  background: url('../assets/check.png') 0 0/cover no-repeat;
}

.checked {
  border: none;
  span { 
    display: inline-block;
  }
}

input {
  opacity: 0;
}


</style>
