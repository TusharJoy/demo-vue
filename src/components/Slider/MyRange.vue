<template>
  <div class='range-slider'>
    <input type="range" :min="minThreshold" :max="maxThreshold" :step="step"
           @input='$emit("update:first", parseInt($event.target.value))' :value='first'
           @change="setBubble('rangeFirst','bubbleF')"
           id="rangeFirst"
    >
    <output id="bubbleF" class="bubbleFirst">{{ first }}</output>
    <!--    <input type="number" v-model="first">-->

    <input type="range" :min="minThreshold" :max="maxThreshold" :step="step"
           @input='$emit("update:second", parseInt($event.target.value))' :value='second'
           @change="setBubble('rangeLast','bubbleLast')"
           id="rangeLast">
    <!--    <input type="number" v-model="second">-->
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
  const min = range.min ? range.min : 0;
  const max = range.max ? range.max : 100;
  const newVal = Number(((val - min) * 100) / (max - min));

  // Sorta magic numbers based on size of the native UI thumb
  bubble.style.left = `calc(${newVal}% + (${8 - newVal * 0.15}px))`;
}
</script>

<style scoped>
.range-slider {
  width: 300px;
  margin: auto;
  text-align: center;
  position: relative;
  height: 6em;
}

.range-slider input[type=range] {
  position: absolute;
  left: 0;
  bottom: 0;
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
  animate: 0.2s;
  background: #2497e3;
  border-radius: 1px;
  box-shadow: none;
  border: 0;
}

input[type=range]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  box-shadow: 0px 0px 0px #000;
  border: 1px solid #2497e3;
  height: 18px;
  width: 18px;
  border-radius: 25px;
  background: #a1d0ff;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -7px;
}

#bubbleF {
  background: red;
  color: white;
  padding: 4px 12px;
  position: absolute;
  border-radius: 4px;
  left: 50%;
  transform: translateX(-50%);
}

#bubbleF::after {
  content: "";
  position: absolute;
  width: 2px;
  height: 2px;
  background: red;
  top: -1px;
  left: 50%;
}

#bubbleLast {
  background: red;
  color: white;
  padding: 4px 12px;
  position: absolute;
  border-radius: 4px;
  left: 50%;
  transform: translateX(-50%);
}

#bubbleLast::after {
  content: "";
  position: absolute;
  width: 2px;
  height: 2px;
  background: red;
  top: -1px;
  left: 50%;
}

</style>