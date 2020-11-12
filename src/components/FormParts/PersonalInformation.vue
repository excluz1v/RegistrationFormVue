<template>
  <div class="personal" @input="globalCheck">
    <CustomInput
      :headText="'ФИО'"
      :allInputs="[
        {
          label: 'Фамилия*',
          inputType: 'text',
          validationData: $v.form.name.lastName,
          atrbts: { maxLength: '30' },
        },
        {
          label: 'Имя*',
          inputType: 'text',
          validationData: $v.form.name.firstName,
          atrbts: { maxLength: '25' },
        },
        {
          label: 'Отчество',
          inputType: 'text',
          validationData: $v.form.name.surName,
          atrbts: { maxLength: '30' },
        },
      ]"
    />
    <CustomInput
      :mounthError="mounthError"
      :headText="'Дата рождения*'"
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
    <CustomInput
      :headText="'Номер телефона*'"
      :allInputs="[
        {
          label: '',
          inputType: 'tel',
          validationData: $v.form.contact.phone,
          atrbts: { maxLength: '11' },
        },
      ]"
    />
    <CustomInput
      :headText="'Пол'"
      :allInputs="[
        {
          label: 'Муж',
          inputType: 'radio',
          validationData: $v.form.gender,
          atrbts: { id: 'male', value: 'male', name: 'gender' },
        },
        {
          label: 'Жен',
          inputType: 'radio',
          validationData: $v.form.gender,
          atrbts: { id: 'female', value: 'female', name: 'gender' },
        },
      ]"
    />
    <CustomSelect
      :headText="'Группа клиентов*'"
      :multiple="true"
      :defaultValue="form.client"
      :allOptions="[
        {
          value: form.clients[0].value,
        },
        {
          value: form.clients[1].value,
        },
        {
          value: form.clients[2].value,
        },
      ]"
    />
    <CustomSelect
      :headText="'Лечащий врач'"
      :multiple="false"
      :allOptions="[
        {
          value: form.doctors[0].value,
        },
        {
          value: form.doctors[1].value,
        },
        {
          value: form.doctors[2].value,
        },
      ]"
    />
    <CustomInput
      :className="'sms'"
      :headText="'Оповещение'"
      :allInputs="[
        {
          label: 'Не отправлять СМС',
          inputType: 'checkbox',
          validationData: $v.form.agreeWIthSMS,
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
  props: ["isValid", "mounthCheck", "mounthError"],
  mixins: [validationMixin],
  validations: {
    form: {
      name: {
        firstName: {
          required,
          minLength: minLength(2),
          RUalpha: helpers.regex("alpha", /^[а-яА-Я]*$/),
        },
        lastName: {
          required,
          minLength: minLength(2),
          RUalpha: helpers.regex("alpha", /^[а-яА-Я]*$/),
        },
        surName: {
          minLength: minLength(2),
          RUalpha: helpers.regex("alpha", /^[а-яА-Я]*$/),
        },
      },
      date: {
        day: {
          required,
          maxValue: maxValue(31),
          minValue: minValue(1),
          numeric,
        },
        mounth: {
          required,
          maxValue: maxValue(12),
          minValue: minValue(1),
          numeric,
        },
        year: {
          required,
          maxValue: maxValue(new Date().getFullYear() - 15),
          minValue: minValue(1920),
          numeric,
        },
      },
      contact: {
        phone: {
          required,
          numeric,
          minLength: minLength(11),
          firstNumber(value) {
            if (+value[0] !== 7) return false;
            else return true;
          },
        },
      },
      gender: {},
      agreeWIthSMS: {},
    },
  },
  data() {
    return {
      form: {
        name: {
          firstName: "",
          lastName: "",
          surName: "",
        },
        date: {
          day: "",
          mounth: "",
          year: "",
        },
        contact: {
          phone: "",
        },
        doctor: "Иванов",
        doctors: [
          {
            label: "Иванов",
            value: "Иванов",
          },
          {
            label: "Захаров",
            value: "Захаров",
          },
          {
            label: "Чернышева",
            value: "Чернышева",
          },
        ],
        client: ["ОСМС"],
        clients: [
          {
            label: "VIP",
            value: "VIP",
          },
          {
            label: "Проблемные",
            value: "Проблемные",
          },
          {
            label: "ОСМС",
            value: "ОСМС",
          },
        ],
        agreeWIthSMS: false,
        gender: "",
      },
    };
  },
  methods: {
    checkValid() {
      this.isValid(this.$v.$invalid);
    },

    globalCheck() {
      this.checkValid();
      this.mounthCheck(
        this.$v.form.date.day.$model,
        this.$v.form.date.mounth.$model
      );
    },
  },
};
</script>

<style lang="scss">
button {
  width: 100px;
  height: 50px;
}
</style>
