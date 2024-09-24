<script setup>
defineProps({
  label: String,
  number: Number,
});
</script>
<template>
  <div class="segment">
    <div class="number-wrapper">
      <transition>
        <span class="numbers absolute top-0 left-[50%]">{{ number }}</span>
      </transition>
    </div>
    <span class="block pt-2 label">{{ label }}</span>
  </div>
</template>
<style scoped>
.segment {
  @apply text-center w-[80px];
}

.number-wrapper {
  @apply relative pt-10 overflow-hidden;
}

.numbers {
  transform: translateX(-50%);
  font-size: 32px;
}

.label {
  font-size: 16px;
}
</style>
