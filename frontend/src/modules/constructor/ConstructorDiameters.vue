<template>
  <label
    v-for="diameter in available"
    :key="diameter.id"
    class="diameter__input diameter__input--small"
  >
    <input
      v-model="selectedDiameter"
      type="radio"
      name="diameter"
      :value="DIAMETERS[diameter.id]"
      class="visually-hidden"
    />
    <span>{{ diameter.name }}</span>
  </label>
</template>

<script setup>
import DIAMETERS from "@/common/data/sizes.js";

import { computed } from "vue";

const props = defineProps({
  modelValue: {
    type: String,
    required: true,
    validator: (v) => Object.values(DIAMETERS).includes(v),
  },
  available: { type: Array, required: true },
});

const emit = defineEmits(["update:modelValue"]);
const selectedDiameter = computed({
  get() {
    return props.modelValue;
  },
  set(newSelectedDiameter) {
    emit("update:modelValue", newSelectedDiameter);
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/app.scss";

.diameter__input {
  margin-right: 8.7%;
  margin-bottom: 20px;
  padding-top: 7px;
  padding-bottom: 6px;
  cursor: pointer;

  span {
    @include r-s16-h19;

    position: relative;
    padding-left: 46px;

    &::before {
      @include p_center_v;

      width: 36px;
      height: 36px;
      content: "";
      transition: 0.3s;
      border-radius: 50%;
      background-color: $green-100;
      background-image: url("@/assets/img/diameter.svg");
      background-repeat: no-repeat;
      background-position: center;
    }
  }

  &:nth-child(3n) {
    margin-right: 0;
  }

  &--small {
    span::before {
      background-size: 18px;
    }
  }

  &--normal {
    span::before {
      background-size: 29px;
    }
  }

  &--big {
    span::before {
      background-size: 100%;
    }
  }

  &:hover {
    span::before {
      box-shadow: $shadow-regular;
    }
  }

  input {
    &:checked + span::before {
      box-shadow: $shadow-large;
    }
  }
}
</style>
