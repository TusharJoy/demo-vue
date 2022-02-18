<script setup>
import MyRange from '@/components/Slider/MyRange.vue';
import {ref} from "vue";

const min = ref(30);
const max = ref(70);
</script>

<template>
  <main>
    <div class="row mt-lg-5">
      <div class="col-3">
      </div>
      <div class="col-lg-3">

      </div>
    </div>
    <div class="row mt-5">
      <div class="row">
        <my-range
            :minThreshold="0"
            :maxThreshold="100"
            :step="1"
            v-model:first="min"
            v-model:second="max">

        </my-range>
      </div>
    </div>

  </main>
</template>
