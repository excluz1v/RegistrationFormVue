<template>
  <div :class="className" class="customInput">
    <div class="formHead">{{ headText }}</div>
    <div class="formBody">
      <label v-for="(newInput, index) in allInputs" :key="index"
        >{{ newInput.label }}
        <input
          :type="newInput.inputType"
          v-model.trim="newInput.validationData.$model"
          v-bind="newInput.atrbts"
          :class="
            newInput.validationData.$error || !!mounthError
              ? 'error'
              : ('' + !newInput.validationData.$error &&
                  newInput.validationData.$model &&
                  newInput.validationData.$dirty) ||
                (mounthError !== undefined && !!mounthError)
              ? 'passed'
              : ''
          "
        />
        <ValidationError
          v-if="newInput.validationData"
          :validationData="newInput.validationData"
        />
        <ValidationError
          v-if="index === 1"
          :mounthError="mounthError"
          :validationData="{}"
        />
      </label>
    </div>
  </div>
</template>

<script>
import ValidationError from "./ValidationError";

export default {
  components: {
    ValidationError,
  },
  props: {
    headText: String,
    allInputs: Array,
    className: String,
    mounthError: String,
  },
};
</script>

<style lang="scss" scoped>
input[type="text"],
input[type="tel"] {
  border: none;
  border-bottom: 0.125rem solid grey;
  font-size: 1.0625rem;
  width: 100%;
  padding: 0.5rem;
  &:hover {
    background-color: rgba(73, 133, 224, 0.12);
    border-color: #121212;
  }
}
.error {
  box-shadow: 1px 1px 10px rgb(255, 0, 43);
}
.passed {
  border-color: #18c56f;
  box-shadow: 0 0 10px rgb(35, 202, 30);
}

@import "./customInput";
</style>
