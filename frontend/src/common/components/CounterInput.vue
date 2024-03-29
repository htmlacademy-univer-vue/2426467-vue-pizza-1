<template>
  <div class="counter-input counter-input--orange">
    <button
      type="button"
      class="counter-input__button counter-input__button--minus"
      :disabled="currentCounter < 1"
      @click="decreaseCounter()"
    >
      <span class="visually-hidden">Меньше</span>
    </button>
    <input
      v-model.number="currentCounter"
      type="text"
      name="counter-input"
      class="counter-input__input"
    />
    <button
      type="button"
      class="counter-input__button counter-input__button--plus"
      @click="increaseCounter()"
    >
      <span class="visually-hidden">Больше</span>
    </button>
  </div>
</template>

<script setup>
import { computed } from "vue";

const NOT_NUMBER_REGEXP = /[^\d]/g;

const emit = defineEmits(["update:modelValue"]);

const props = defineProps({
  modelValue: { type: Number, required: true },
});

const currentCounter = computed({
  get() {
    return props.modelValue;
  },
  set(newCounterValue) {
    let newCounterValueSafe = 0;
    if (typeof newCounterValue === "number") {
      newCounterValueSafe = newCounterValue;
    } else if (typeof newCounterValue === "string") {
      newCounterValueSafe = Number(
        newCounterValue.replace(NOT_NUMBER_REGEXP, "")
      );
    }

    emit("update:modelValue", newCounterValueSafe);
  },
});

function increaseCounter() {
  currentCounter.value += 1;
}

function decreaseCounter() {
  currentCounter.value -= 1;
}
</script>

<style lang="scss" scoped>
@import "@/assets/scss/app.scss";

.counter-input {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.counter-input__button {
  $el: &;
  $size_icon: 50%;

  position: relative;
  display: block;
  width: 16px;
  height: 16px;
  margin: 0;
  padding: 0;
  cursor: pointer;
  transition: 0.3s;
  border: none;
  border-radius: 50%;
  outline: none;

  &--minus {
    background-color: $purple-100;

    &::before {
      @include p_center-all;

      width: $size_icon;
      height: 2px;
      content: "";
      border-radius: 2px;
      background-color: $black;
    }

    &:hover:not(:active):not(:disabled) {
      background-color: $purple-200;
    }

    &:active:not(:disabled) {
      background-color: $purple-300;
    }

    &:focus:not(:disabled) {
      box-shadow: $shadow-regular;
    }

    &:disabled {
      cursor: default;

      &::before {
        opacity: 0.1;
      }
    }
  }

  &--plus {
    background-color: $green-500;

    &::before {
      @include p_center-all;

      width: $size_icon;
      height: 2px;
      content: "";
      border-radius: 2px;
      background-color: $white;
    }

    &::after {
      @include p_center-all;

      width: $size_icon;
      height: 2px;
      content: "";
      transform: translate(-50%, -50%) rotate(90deg);
      border-radius: 2px;
      background-color: $white;
    }

    &:hover:not(:active):not(:disabled) {
      background-color: $green-400;
    }

    &:active:not(:disabled) {
      background-color: $green-600;
    }

    &:focus:not(:disabled) {
      box-shadow: $shadow-regular;
    }

    &:disabled {
      cursor: default;
      opacity: 0.3;
    }
  }

  &--orange {
    background-color: $orange-200;

    &:hover:not(:active):not(:disabled) {
      background-color: $orange-100;
    }

    &:active:not(:disabled) {
      background-color: $orange-300;
    }
  }
}

.counter-input__input {
  @include r-s14-h16;

  box-sizing: border-box;
  width: 22px;
  margin: 0;
  padding: 0 3px;
  text-align: center;
  color: $black;
  border: none;
  border-radius: 10px;
  outline: none;
  background-color: transparent;

  &:focus {
    box-shadow: inset $shadow-regular;
  }
}
</style>
