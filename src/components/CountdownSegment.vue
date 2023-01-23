<script setup>
defineProps({
  label: String,
  number: Number,
})
</script>
<template>
  <div class="segment text-center">
    <div class="pt-10 overflow-hidden relative">
      <Transition name="slide-up">
        <span :key="number" class="numbers text-green absolute top-0 left-[50%]">{{ number }}</span>
      </Transition>
    </div>
    <span class="label block pt-2">{{ label }}</span>
  </div>
</template>
<style>
.segment {
  width: 80px;
}
.numbers {
  transform: translateX(-50%);
  font-size: 32px;
}
.label {
  font-size: 16px;
}

.slide-up-enter-active,
.slide-up-leave-active {
  transition: all .5s ease;
}

.slide-up-enter-from {
  transform: translateY(100%)  translateX(-50%);
}

.slide-up-enter-to,
.slide-up-leave-from {
  transform: translateY(0px)  translateX(-50%);
}

.slide-up-leave-to {
  transform: translateY(-100%) translateX(-50%);
}

</style>
