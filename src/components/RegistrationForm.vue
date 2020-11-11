<template>
  <form class="registration" @submit="submit" @input="completeChanger">
    <PersonalInformation :isValid="isPersonalInformationValid" />
    <Adress :isValid="isAdressValid" />
    <Passport :isValid="isPassportValid" />
    <button type="submit" class="submit" :disabled="!complete">
      Зарегистрироваться
    </button>
    <div v-if="!completeMsg" class="modal">
      <div>Вы успешно зарегистрированы</div>
      <button @click="closeModal">OK</button>
    </div>
  </form>
</template>

<script>
import PersonalInformation from "./FormParts/PersonalInformation";
import Adress from "./FormParts/Adress";
import Passport from "./FormParts/Passport";

export default {
  components: {
    PersonalInformation,
    Adress,
    Passport,
  },
  methods: {
    submit() {
      event.preventDefault();
      this.$data.completeMsg = true;
      console.log(this.$data.completeMsg);
    },
    isPersonalInformationValid(data) {
      this.$data.personalInformation = !data;
    },
    isAdressValid(data) {
      this.$data.adress = !data;
    },
    isPassportValid(data) {
      this.$data.passport = !data;
    },
    completeChanger() {
      this.$data.complete = [
        this.$data.personalInformation,
        this.$data.adress,
        this.$data.passport,
      ].every((el) => el === true);
    },
    closeModal() {
      this.$data.completeMsg = false;
    },
  },
  data() {
    return {
      personalInformation: false,
      adress: false,
      passport: false,
      complete: false,
      completeMsg: true,
    };
  },
};
</script>

<style lang="scss">
.registration {
  display: flex;
  flex-wrap: wrap;
  & > div {
    margin-top: 15px;
    border: 1px solid #ddd;
  }
  button {
    width: 150px;
    height: 30px;
  }
}
.modal {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: fixed;
  align-items: center;
  width: 25%;
  height: 50vh;
  background-color: rgb(120, 223, 106);
  z-index: 2;
  text-align: center;
  border-radius: 10px;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  padding: 10px 20px;

  div {
    border: none;
  }
}
.submit {
  margin: 15px auto;
  background-color: #78df6a;
  &:disabled {
    background-color: #ddd;
  }
}
</style>
