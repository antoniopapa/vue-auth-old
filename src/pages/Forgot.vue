<template>
  <form class="form-signin" @submit.prevent="submit">
    <div v-if="notify.cls" :class="`alert alert-${notify.cls}`" role="alert">
      {{ notify.message }}
    </div>

    <h1 class="h3 mb-3 font-weight-normal">Please set your email</h1>

    <input v-model="email" type="email" class="form-control mb-3" placeholder="Email" required>

    <button class="btn btn-lg btn-primary btn-block" type="submit">Submit</button>
  </form>
</template>

<script>
import {ref, reactive} from 'vue';
import axios from 'axios';

export default {
  name: "Forgot",
  setup() {
    const email = ref('');
    const notify = reactive({
      cls: '',
      message: ''
    });

    const submit = async () => {
      try {
        await axios.post('forgot', {
          email: email.value
        });

        notify.cls = 'success';
        notify.message = 'Email was sent!';
      } catch (e) {
        notify.cls = 'danger';
        notify.message = 'Email does not exist!';
      }
    }

    return {
      email,
      notify,
      submit
    }
  }
}
</script>

