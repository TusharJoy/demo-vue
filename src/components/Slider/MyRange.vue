<template>
  <div class="slider">
    <div class="pro" :style="{ 'left': leftLength,'right':rightLength }"></div>
  </div>
  <div class="range-slider">
    <output id="bubbleF" class="bubbleFirst" :class="{'bubbleActive':firstBubbleActive}">{{ first }}</output>
    <input
        type="range"
        :min="minThreshold"
        :max="maxThreshold"
        :step="step"
        @input="$emit('update:first', parseInt($event.target.value));setFirstActive();setRangeColor();"

        :value="first"
        id="rangeFirst"
    />

    <input
        type="range"
        :min="minThreshold"
        :max="maxThreshold"
        :step="step"
        @input="$emit('update:second', parseInt($event.target.value));setLastActive();setRangeColor();"
        :value="second"
        id="rangeLast"
    />

    <output id="bubbleLast" :class="{'bubbleActive':lastBubbleActive}" class="bubble">{{ second }}</output>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from "vue";

const myProps = defineProps({
  minThreshold: {
    type: Number,
    default: -100,
  },
  maxThreshold: {
    type: Number,
    default: 100,
  },
  step: {
    type: Number,
    default: 1,
  },
  first: {
    type: Number,
    default: 10,
  },
  second: {
    type: Number,
    default: 80,
  },
});

let firstBubbleActive = ref(0)
let lastBubbleActive = ref(0);

let setLastActive = () => {
  lastBubbleActive.value = 1;
  firstBubbleActive.value = 0;
}
let setFirstActive = () => {
  firstBubbleActive.value = 1;
  lastBubbleActive.value = 0;
}

onMounted(() => {
  setBubble("rangeFirst", "bubbleF");
  setBubble("rangeLast", "bubbleLast");
  setRangeColor()
});

const leftLength = computed(
    () => {
      return (myProps.first / myProps.maxThreshold) * 100 + "%";
    }
)

const rightLength = computed(() => {
  return 100 - (myProps.second / myProps.maxThreshold) * 100 + "%";
})

const setRangeColor = () => {
  const progress = document.querySelector(".slider .pro");
  progress.style.left = leftLength.value;
  progress.style.right = rightLength.value;
}


const setBubble = (rangeId, bubbleId) => {
  const range = document.getElementById(rangeId);
  const bubble = document.getElementById(bubbleId);
  const val = range.value;
  const min = 0;
  const max = 100;
  const newVal = Number(((val - min) * 100) / (max - min));
  bubble.style.left = `calc(${newVal}% + (${8 - newVal * 0.15}px))`;

};

</script>

<style scoped>
.slider {
  height: 4px;
  background: #248286;
  position: relative;
  top: 12px;
  max-width: 400px;
}
.slider .pro {
  height: 4px;
  left: 32%;
  right: 32%;
  position: absolute;
  background: #ffcf67;
}
.range-slider {
  display: inline-block;
  max-width: 400px;
  width: 100%;
  margin: auto;
  text-align: center;
  position: relative;
  height: 10px;
}

.range-slider input[type="range"] {
  position: absolute;
  left: 0;
  background: none;
}

input[type="range"] {
  -webkit-appearance: none;
  width: 100%;
}

input[type="range"]:focus {
  outline: none;
}

/* input[type=range]:focus::-webkit-slider-runnable-track {
  background: #FFCF67;
} */

input[type="range"]:focus::-ms-fill-lower {
  background: #ffcf67;
}

input[type="range"]:focus::-ms-fill-upper {
  background: #ffcf67;
}

input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 4px;
  cursor: pointer;
  background: none;
  box-shadow: none;
  border: 0;
}

input[type="range"]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  box-shadow: 0px 0px 0px #000;
  border: 1px solid #ffcf67;
  height: 18px;
  width: 18px;
  border-radius: 25px;
  background: #ffcf67;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -7px;
}

input[type="range"]::-webkit-slider-thumb:hover {
  transform: scale(2.2);
  border: 3px solid #adb778;
  border-radius: 50%;
}

.bubbleActive {
  background: #ffcf67 !important;
  color: #299196 !important;
  border: none !important;
}

#bubbleF {
  background: transparent;
  border: 2px solid #ffff;
  color: white;
  font-weight: bold;
  padding: 6px 12px;
  position: absolute;
  border-radius: 15px;
  left: -90px !important;
  top: -10px;
}
#bubbleLast {
  background: transparent;
  border: 2px solid #ffff;
  font-weight: bold;
  color: white;
  padding: 3px 12px;
  position: absolute;
  border-radius: 17px;
  top: -10px;
  right: -90px;
  left: unset !important;
}
</style>
