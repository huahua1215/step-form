<script setup>
import { ref } from "vue";

const step = ref(1);

const next = () => {
  if (step.value > 3) {
    step.value = 3;
  } else {
    step.value++;
  }
};
const back = () => {
  if (step.value < 2) {
    step.value = 1;
  } else {
    step.value--;
  }
};
</script>

<template>
  <div class="flex">
    <div
      class="step"
      :class="{ 'step-active': step === 1, 'step-done': step > 1 }"
    >
      1
    </div>
    <div
      class="step"
      :class="{ 'step-active': step === 2, 'step-done': step > 2 }"
    >
      2
    </div>
    <div
      class="step"
      :class="{ 'step-active': step === 3, 'step-done': step > 3 }"
    >
      3
    </div>
    <button @click.prevent="back">前進</button>
    <button @click.prevent="next">後退</button>
  </div>
  <div v-show="step === 1">區塊一</div>
  <div v-show="step === 2">區塊二</div>
  <div v-show="step === 3">區塊三</div>
</template>

<style scoped>
.step {
  background-color: rgb(175, 175, 175);
  color: aliceblue;
  margin: 0 20px;
  padding: 30px;
  border-radius: 50%;
}
.step-active,
.step-done {
  background-color: black;
}
</style>
