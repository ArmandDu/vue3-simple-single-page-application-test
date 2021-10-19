<!--

This component is a test with:

- vue-class-component
- this.$emit
- form component
- v-submit.prevent directive

TODO: validation

-->
<template>
  <form id="user-form" @submit.prevent="submit">
    <input placeholder="Full Name" v-model="name"/>
    <input placeholder="E-mail address" v-model="email" type="email"/>
    <input placeholder="Phone number" v-model="phone" type="tel"/>
    <button type="submit">Add new</button>
  </form>
</template>

<script lang="ts">
import {Options, Vue} from "vue-class-component";

@Options({
  emits: ["new-participant"]
})

export default class AddParticipant extends Vue {
  name = ""
  email = ""
  phone = ""


  submit() {

    //TODO validation
    this.$emit('new-participant', {email: this.email, name: this.name, phone: this.phone})

    this.name = "";
    this.phone = "";
    this.email = "";
  }

}
</script>

<style scoped lang="scss">

#user-form {
  display: flex;
  background-color: white;
  margin: 8px;

  width: 100%;

  input {
    margin: 16px;
  }

}

</style>