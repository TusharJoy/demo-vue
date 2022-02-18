<script setup>
import MyRange from '@/components/Slider/MyRange.vue';
import {ref} from "vue";

const min = ref(30);
const max = ref(70);
</script>

<template>
<div class="main_wrapper">
  <main class="container">
      <div class="row mt-5">
        <div class="col-md-2">
          <div class="title">Age ranges: </div>
        </div>
        <div class="col-md-3">
          <button class='common-btn'>All years</button>
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
  </main>
</div>
</template>

<style scoped>

/* todo: this is for now you to show the exact design*/
.main_wrapper{
  height: 50vh;
  background: #299196;
  display: flex;
  justify-content: center;
  align-items: center;
}

.title {
  font-weight: bold;
  font-size: 18px;
  color: #ffff;
}

.common-btn {
  font-weight: bold;
  max-width: 100px;
  padding: 5px 14px;
  border-radius: 25px;
  border: 2px solid #fff;
  color: #ffff;
  background: transparent;
}

</style>