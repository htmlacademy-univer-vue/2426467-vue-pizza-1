<template>
  <div class="ingredients__filling">
    <p>Начинка:</p>
    <ul class="ingredients__list">
      <li
        v-for="ingredient in available"
        :key="ingredient.id"
        class="ingredients__item"
      >
        <span :class="`filling filling--${INGREDIENTS[ingredient.id]}`">{{
          ingredient.name
        }}</span>
        <counter-input
          class="ingredients__counter"
          :model-value="ingredientsAmounts[INGREDIENTS[ingredient.id]].amount"
          @update:model-value="
            setIngredientCount(INGREDIENTS[ingredient.id], $event)
          "
        />
      </li>
    </ul>
  </div>
</template>

<script setup>
import INGREDIENTS from "@/common/data/ingredients.js";

import { computed } from "vue";
import { CounterInput } from "@/common/components";

const props = defineProps({
  modelValue: { type: Object, required: true },
  available: { type: Array, required: true },
});
const emit = defineEmits(["update:modelValue"]);

const ingredientsAmounts = computed(() => props.modelValue);

function setIngredientCount(ingredient, newAmount) {
  emit("update:modelValue", {
    ...ingredientsAmounts.value,
    [ingredient]: { amount: newAmount },
  });
}
</script>

<style lang="scss" scoped>
@import "@/assets/scss/app.scss";

.ingredients__filling {
  width: 100%;

  p {
    @include r-s16-h19;

    margin-top: 0;
    margin-bottom: 16px;
  }
}

.ingredients__list {
  @include clear-list;

  display: flex;
  align-items: flex-start;
  flex-wrap: wrap;
}

.ingredients__item {
  width: 100px;
  min-height: 40px;
  margin-right: 17px;
  margin-bottom: 35px;
}

.ingredients__counter {
  width: 54px;
  margin-top: 10px;
  margin-left: 36px;
}

.filling {
  @include r-s14-h16;
  position: relative;
  display: block;
  padding-left: 36px;

  &::before {
    @include p_center-v;

    display: block;
    width: 32px;
    height: 32px;
    content: "";
    border-radius: 50%;
    background-color: $white;
    background-repeat: no-repeat;
    background-position: center;
    background-size: 80% 80%;
  }

  &--tomatoes::before {
    background-image: url("@/assets/img/filling/tomatoes.svg");
  }

  &--ananas::before {
    background-image: url("@/assets/img/filling/ananas.svg");
  }

  &--bacon::before {
    background-image: url("@/assets/img/filling/bacon.svg");
  }

  &--blue_cheese::before {
    background-image: url("@/assets/img/filling/blue_cheese.svg");
  }

  &--cheddar::before {
    background-image: url("@/assets/img/filling/cheddar.svg");
  }

  &--chile::before {
    background-image: url("@/assets/img/filling/chile.svg");
  }

  &--ham::before {
    background-image: url("@/assets/img/filling/ham.svg");
  }

  &--jalapeno::before {
    background-image: url("@/assets/img/filling/jalapeno.svg");
  }

  &--mozzarella::before {
    background-image: url("@/assets/img/filling/mozzarella.svg");
  }

  &--mushrooms::before {
    background-image: url("@/assets/img/filling/mushrooms.svg");
  }

  &--olives::before {
    background-image: url("@/assets/img/filling/olives.svg");
  }

  &--onion::before {
    background-image: url("@/assets/img/filling/onion.svg");
  }

  &--parmesan::before {
    background-image: url("@/assets/img/filling/parmesan.svg");
  }

  &--salami::before {
    background-image: url("@/assets/img/filling/salami.svg");
  }

  &--salmon::before {
    background-image: url("@/assets/img/filling/salmon.svg");
  }
}
</style>
