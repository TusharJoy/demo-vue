<template>
  <button class="common-btn">
    <slot></slot> <!-- slot outlet -->
  </button>
</template>

<script setup>

</script>
<style scoped>
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