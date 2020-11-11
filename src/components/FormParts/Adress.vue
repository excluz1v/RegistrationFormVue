<template>
  <div class="adress" @input="check">
    <CustomInput
      :headText="'Адрес*'"
      :allInputs="[
        {
          label: 'Индекс',
          inputType: 'text',
          validationData: $v.form.adress.postIndex,
          atrbts: { maxLength: '16' },
        },
        {
          label: 'Страна',
          inputType: 'text',
          validationData: $v.form.adress.country,
          atrbts: { maxLength: '20' },
        },
      ]"
    />
    <CustomInput
      :headText="''"
      :allInputs="[
        {
          label: 'Область',
          inputType: 'text',
          validationData: $v.form.adress.region,
          atrbts: { maxLength: '25' },
        },
        {
          label: 'Город*',
          inputType: 'text',
          validationData: $v.form.adress.city,
          atrbts: { maxLength: '20' },
        },
        {
          label: 'Улица',
          inputType: 'text',
          validationData: $v.form.adress.street,
          atrbts: { maxLength: '20' },
        },
        {
          label: 'Дом',
          inputType: 'text',
          validationData: $v.form.adress.house,
          atrbts: { maxLength: '3' },
        },
      ]"
    />
  </div>
</template>

<script>
import { validationMixin } from "vuelidate";
import {
  required,
  minLength,
  maxValue,
  minValue,
  numeric,
  helpers,
} from "vuelidate/lib/validators";
import CustomInput from "../FormGenerators/CustomInput";

export default {
  components: {
    CustomInput,
  },
  props: ["isValid"],
  mixins: [validationMixin],
  validations: {
    form: {
      adress: {
        postIndex: { numeric, minLength: minLength(6) },
        country: {
          RUalpha: helpers.regex("alpha", /^[а-яА-Я]*$/),
          minLength: minLength(3),
        },
        region: {
          RUalpha: helpers.regex("alpha", /^[а-яА-Я]*$/),
          minLength: minLength(3),
        },
        city: {
          required,
          RUalpha: helpers.regex("alpha", /^[а-яА-Я]*$/),
          minLength: minLength(3),
        },
        street: {
          RUalpha: helpers.regex("alpha", /^[а-яА-Я]*$/),
          minLength: minLength(3),
        },
        house: { minValue: minValue(1), numeric, maxValue: maxValue(500) },
      },
    },
  },
  data() {
    return {
      form: {
        adress: {
          postIndex: "",
          country: "",
          region: "",
          city: "",
          street: "",
          house: "",
        },
      },
    };
  },
  methods: {
    check() {
      this.isValid(this.$v.$invalid);
    },
  },
};
</script>

<style lang="scss"></style>
