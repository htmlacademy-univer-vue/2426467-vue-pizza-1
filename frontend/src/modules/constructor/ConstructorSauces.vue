<template>
  <div class="ingredients__sauce">
    <p>Основной соус:</p>
    <radio-button
      v-for="sauce in available"
      :key="sauce.id"
      v-model="selectedSauce"
      class="ingredients__input"
      name="sauce"
      :value="SAUCES[sauce.id]"
    >
      {{ sauce.name }}
    </radio-button>
  </div>
</template>

<script setup>
import SAUCES from "@/common/data/sauces.js";

import { computed } from "vue";
import { RadioButton } from "@/common/components";

const props = defineProps({
  modelValue: {
    type: String,
    required: true,
    validator: (v) => Object.values(SAUCES).includes(v),
  },
  available: { type: Array, required: true },
});

const emit = defineEmits(["update:modelValue"]);
const selectedSauce = computed({
  get() {
    return props.modelValue;
  },
  set(newSelectedSauce) {
    emit("update:modelValue", newSelectedSauce);
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/app.scss";

.ingredients__input {
  margin-right: 24px;
  margin-bottom: 10px;
}

.ingredients__sauce {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  width: 100%;
  margin-bottom: 14px;

  p {
    @include r-s16-h19;

    margin-top: 0;
    margin-right: 16px;
    margin-bottom: 10px;
  }
}
</style>
