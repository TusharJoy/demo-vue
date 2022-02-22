<template>
  <div class="row mt-5">
    <div class="col-md-2">
      <div class="title">Age ranges:</div>
    </div>
    <div class="col-md-3">
      <my-button @click="setAllRange">
        All years
      </my-button>
    </div>

    <div class="col-md-7">
      <my-range
          :minThreshold="0"
          :maxThreshold="100"
          :step="1"
          v-model:first="min"
          v-model:second="max">
      </my-range>
    </div>
  </div>
</template>

<script setup>
import MyRange from '@/components/Slider/MyRange.vue';
import {ref} from "vue";
import MyButton from "@/components/Button/MyButton.vue";

const min = ref(30);
const max = ref(70);
const minThreshold = ref(0);
const maxThreshold = ref(100);

const setAllRange = () => {
  min.value = minThreshold.value;
  max.value = maxThreshold.value;
}

</script>

<style scoped>
.title {
  font-weight: bold;
  font-size: 18px;
  color: #ffff;
}
</style>