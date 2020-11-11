<template>
  <div class="passport" @input="check">
    <CustomSelect
      :headText="'Тип документа'"
      :multiple="false"
      :defaultValue="form.document"
      :allOptions="[
        {
          value: form.documentType[0].value,
        },
        {
          value: form.documentType[1].value,
        },
        {
          value: form.documentType[2].value,
        },
      ]"
    />
    <CustomInput
      :headText="'Документ'"
      :allInputs="[
        {
          label: 'Серия',
          inputType: 'text',
          validationData: $v.form.serialNumber,
          atrbts: { maxLength: '4' },
        },
        {
          label: 'Номер',
          inputType: 'text',
          validationData: $v.form.registationNumber,
          atrbts: { maxLength: '8' },
        },
        {
          label: 'Кем выдан ',
          inputType: 'text',
          validationData: $v.form.byWhoWasGiven,
          atrbts: { maxLength: '21' },
        },
      ]"
    />
    <CustomInput
      :headText="'Дата выдачи*'"
      :className="'date'"
      :allInputs="[
        {
          label: 'День',
          inputType: 'text',
          validationData: $v.form.date.day,
          atrbts: { maxLength: '2' },
        },
        {
          label: 'Месяц',
          inputType: 'text',
          validationData: $v.form.date.mounth,
          atrbts: { maxLength: '2' },
        },
        {
          label: 'Год',
          inputType: 'text',
          validationData: $v.form.date.year,
          atrbts: { maxLength: '4' },
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
import CustomSelect from "../FormGenerators/CustomSelect";

export default {
  components: {
    CustomInput,
    CustomSelect,
  },
  props: ["isValid"],
  mixins: [validationMixin],
  validations: {
    form: {
      date: {
        day: {
          required,
          maxValue: maxValue(31),
          minValue: minValue(1),
          minLength: minLength(2),
          numeric,
        },
        mounth: {
          required,
          maxValue: maxValue(12),
          minValue: minValue(1),
          minLength: minLength(2),
          numeric,
        },
        year: {
          required,
          maxValue: maxValue(new Date().getFullYear() - 15),
          minValue: minValue(1920),
          minLength: minLength(4),
          numeric,
        },
      },
      serialNumber: {
        minLength: minLength(4),
        onlyEngAndNumbers: helpers.regex("alpha", /^[a-zA-Z0-9]*$/),
      },
      registationNumber: { numeric, minLength: minLength(5) },
      byWhoWasGiven: {
        alpha: helpers.regex("alpha", /^[а-яА-Яa-zA-Z]*$/),
        minLength: minLength(3),
      },
    },
  },
  data() {
    return {
      form: {
        document: ["Паспорт"],
        documentType: [
          {
            label: "Паспорт",
            value: "Паспорт",
          },
          {
            label: "Свид. о рождении",
            value: "Свид. о рождении",
          },
          {
            label: "Вод. удостоверение",
            value: "Вод. удостоверение",
          },
        ],
        serialNumber: "",
        registationNumber: "",
        byWhoWasGiven: "",
        date: {
          day: "",
          mounth: "",
          year: "",
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
