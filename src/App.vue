<template>
  <div id="app">
    <RegistrationForm />
  </div>
</template>

<script>
import RegistrationForm from "./components/RegistrationForm";
export default {
  name: "App",
  components: {
    RegistrationForm,
  },
};
</script>

<style lang="scss">
@import "./style/app";
</style>
