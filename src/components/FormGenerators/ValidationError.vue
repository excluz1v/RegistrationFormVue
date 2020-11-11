<template>
  <ul>
    <li
      v-if="
        validationData.required !== undefined &&
          !validationData.required &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      Обязательно
    </li>
    <li
      v-if="
        validationData.minLength !== undefined &&
          !validationData.minLength &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      {{ `Длина не менее ${validationData.$params.minLength.min}  символов` }}
    </li>
    <li
      v-if="
        validationData.RUalpha !== undefined &&
          !validationData.RUalpha &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      Только Кириллица
    </li>
    <li
      v-if="
        validationData.alpha !== undefined &&
          !validationData.alpha &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      Только буквы
    </li>
    <li
      v-if="
        validationData.onlyEngAndNumbers !== undefined &&
          !validationData.onlyEngAndNumbers &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      Только Латиница и цифры
    </li>
    <li
      v-if="
        validationData.numeric !== undefined &&
          !validationData.numeric &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      Только цифры
    </li>
    <li
      v-if="
        validationData.maxValue !== undefined &&
          !validationData.maxValue &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      {{ `Число не более ${validationData.$params.maxValue.max}` }}
    </li>
    <li
      v-if="
        validationData.minValue !== undefined &&
          !validationData.minValue &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      {{ `Число не менее ${validationData.$params.minValue.min}` }}
    </li>
    <li
      v-if="
        validationData.firstNumber !== undefined &&
          !validationData.firstNumber &&
          validationData.$dirty
      "
      :class="validationData.$error ? 'isInvalid' : ''"
    >
      {{ "Номер должен начинаться с 7" }}
    </li>
  </ul>
</template>

<script>
export default {
  props: { validationData: Object },
};
</script>

<style scoped lang="scss">
li {
  font-size: 0.9rem;
  margin-bottom: 5px;
}
.isInvalid {
  color: red;
}
</style>
