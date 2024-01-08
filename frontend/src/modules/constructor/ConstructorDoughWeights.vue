<template>
  <label
    v-for="doughWeight in available"
    :key="doughWeight.id"
    class="dough__input dough__input--light"
  >
    <input
      v-model="selectedDough"
      type="radio"
      name="dought"
      :value="DOUGH_WEIGHTS[doughWeight.id]"
      class="visually-hidden"
    />
    <b>{{ doughWeight.name }}</b>
    <span>{{ doughWeight.description }}</span>
  </label>
</template>

<script setup>
import DOUGH_WEIGHTS from "@/common/data/doughSizes.js";

import { computed } from "vue";

const props = defineProps({
  modelValue: {
    type: String,
    required: true,
    validator: (v) => Object.values(DOUGH_WEIGHTS).includes(v),
  },
  available: { type: Array, required: true },
});

const emit = defineEmits(["update:modelValue"]);
const selectedDough = computed({
  get() {
    return props.modelValue;
  },
  set(newSelectedDough) {
    emit("update:modelValue", newSelectedDough);
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/app.scss";

.dough__input {
  position: relative;
  margin-right: 8%;
  margin-bottom: 20px;
  padding-left: 50px;
  cursor: pointer;

  b {
    @include r-s16-h19;

    &::before {
      @include p_center-v;

      width: 36px;
      height: 36px;
      content: "";
      transition: 0.3s;
      border-radius: 50%;
      background-repeat: no-repeat;
      background-position: center;
      background-size: cover;
    }
  }

  span {
    @include l-s11-h13;

    display: block;
  }

  &--light {
    b {
      &::before {
        background-image: url("@/assets/img/dough-light.svg");
      }
    }
  }

  &--large {
    b {
      &::before {
        background-image: url("@/assets/img/dough-large.svg");
      }
    }
  }

  &:hover {
    b::before {
      box-shadow: $shadow-regular;
    }
  }

  input {
    &:checked + b::before {
      box-shadow: $shadow-large;
    }
  }
}
</style>
