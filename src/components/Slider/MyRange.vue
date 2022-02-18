<template>
  <div class='range-slider'>
    <output id="bubbleF" class="bubbleFirst">{{ first }}</output>
    <input type="range" :min="minThreshold" :max="maxThreshold" :step="step"
           @input="$emit('update:first', parseInt($event.target.value))"
           :value='first'
           id="rangeFirst">
   
    <input type="range" :min="minThreshold" :max="maxThreshold" :step="step"
           @input="$emit('update:second', parseInt($event.target.value))" :value='second'
           id="rangeLast">

    <output  id="bubbleLast" class="bubble">{{ second }}</output>
  </div>
</template>

<script setup>

import {onMounted} from "vue";

defineProps({
  minThreshold: {
    type: Number,
    default: -100
  },
  maxThreshold: {
    type: Number,
    default: 100
  },
  step: {
    type: Number,
    default: 1
  },
  first: {
    type: Number,
    default: 10
  },
  second: {
    type: Number,
    default: 80
  }
})
onMounted(() => {
  setBubble('rangeFirst','bubbleF')
  setBubble('rangeLast','bubbleLast')
})

const setBubble = (rangeId, bubbleId) => {

  const range = document.getElementById(rangeId);
  const bubble = document.getElementById(bubbleId);
  const val = range.value;
  const min =  0;
  const max =  100;
  const newVal = Number(((val - min) * 100) / (max - min));

  // Sorta magic numbers based on size of the native UI thumb
  bubble.style.left = `calc(${newVal}% + (${8 - newVal * 0.15}px))`;
}
</script>

<style scoped>
.range-slider {
  display: inline-block;
  max-width: 400px;
  width: 100%;
  margin: auto;
  text-align: center;
  position: relative;
  height: 10px;
}

.range-slider input[type=range] {
  position: absolute;
  left: 0;
}

input[type=range] {
  -webkit-appearance: none;
  width: 100%;
}

input[type=range]:focus {
  outline: none;
}

input[type=range]:focus::-webkit-slider-runnable-track {
  background: #2497e3;
}

input[type=range]:focus::-ms-fill-lower {
  background: #2497e3;
}

input[type=range]:focus::-ms-fill-upper {
  background: #2497e3;
}

input[type=range]::-webkit-slider-runnable-track {
  width: 100%;
  height: 5px;
  cursor: pointer;
  /* animate: 0.2s; */
  background: #2497e3;
  border-radius: 1px;
  box-shadow: none;
  border: 0;
}

input[type=range]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  box-shadow: 0px 0px 0px #000;
  border: 1px solid #FFCF67;
  height: 18px;
  width: 18px;
  border-radius: 25px;
  background: #FFCF67;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -7px;
}

#bubbleF {
  background: #FFCF67;
  color: #299196;
  font-weight: bold;
  padding: 6px 12px;
  position: absolute;
  border-radius: 15px;
  left: -90px !important;
  top: -10px;
}

/* #bubbleF::after {
  content: "";
  position: absolute;
  width: 2px;
  height: 2px;
  background: #FFCF67;
  top: -1px;
  left: 50%;
} */

#bubbleLast {
  background: transparent;
  border: 2px solid #ffff;
  font-weight: bold;
  color: white;
  padding: 6px 12px;
  position: absolute;
  border-radius: 17px;
  top: -10px;
  right: -90px;
  left: unset !important;
}

/* #bubbleLast::after {
  content: "";
  position: absolute;
  width: 2px;
  height: 2px;
  background: #ffff;
  top: -1px;
  left: 50%;
} */

</style>