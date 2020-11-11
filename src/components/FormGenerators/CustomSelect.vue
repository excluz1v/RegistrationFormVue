<template>
  <div :class="className" class="customInput">
    <div class="formHead">{{ headText }}</div>
    <div class="formBody">
      <select :multiple="multiple" :value="defaultValue">
        <option
          v-for="(newOption, index) in allOptions"
          :key="index"
          v-bind="newOption.atrbts"
          :value="newOption.value"
          >{{ newOption.value }}
        </option>
      </select>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    headText: String,
    allOptions: Array,
    className: String,
    multiple: Boolean,
    defaultValue: Array,
  },
};
</script>

<style lang="scss">
@import "./customSelect";
</style>
