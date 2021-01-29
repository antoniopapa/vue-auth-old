<template>
  <form class="form-signin" @submit.prevent="submit">
    <h1 class="h3 mb-3 font-weight-normal">Please register</h1>

    <input v-model="firstName" class="form-control" placeholder="First Name" required>

    <input v-model="lastName" class="form-control" placeholder="Last Name" required>

    <input v-model="email" type="email" class="form-control" placeholder="Email" required>

    <input v-model="password" type="password" class="form-control" placeholder="Password" required>

    <input v-model="passwordConfirm" type="password" class="form-control" placeholder="Password Confirm" required>

    <button class="btn btn-lg btn-primary btn-block" type="submit">Submit</button>
  </form>
</template>

<script>
import {ref} from 'vue';
import axios from 'axios'
import {useRouter} from "vue-router";

export default {
  name: "Register",
  setup() {
    const firstName = ref('');
    const lastName = ref('');
    const email = ref('');
    const password = ref('');
    const passwordConfirm = ref('');
    const router = useRouter();

    const submit = async () => {
      await axios.post('register', {
        first_name: firstName.value,
        last_name: lastName.value,
        email: email.value,
        password: password.value,
        password_confirm: passwordConfirm.value
      });

      await router.push('/login');
    }

    return {
      firstName,
      lastName,
      email,
      password,
      passwordConfirm,
      submit
    }
  }
}
</script>
