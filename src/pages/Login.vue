<template>
  <form class="form-signin" @submit.prevent="submit">
    <h1 class="h3 mb-3 font-weight-normal">Please sign in</h1>

    <input v-model="email" type="email" class="form-control" placeholder="Email" required>

    <input v-model="password" type="password" class="form-control" placeholder="Password" required>

    <div class="mb-2">
      <router-link to="/forgot">Forgot Password?</router-link>
    </div>

    <button class="btn btn-lg btn-primary btn-block" type="submit">Submit</button>
  </form>
</template>

<script>
import {ref} from 'vue';
import axios from 'axios';
import {useRouter} from "vue-router";

export default {
  name: "Login",
  setup() {
    const email = ref('');
    const password = ref('');
    const router = useRouter();

    const submit = async () => {
      await axios.post('login', {
        email: email.value,
        password: password.value
      });

      await router.push('/');
    }

    return {
      email,
      password,
      submit
    }
  }
}
</script>
