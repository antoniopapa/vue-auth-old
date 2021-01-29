<template>
  <nav class="navbar navbar-expand-md navbar-dark bg-dark">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item">
        <router-link to="/" class="nav-link">Home</router-link>
      </li>
    </ul>

    <ul class="navbar-nav my-2 my-lg-0">
      <li class="nav-item" v-if="auth">
        <a href="#" class="nav-link" @click="logout">Logout</a>
      </li>

      <template v-if="!auth">
        <li class="nav-item">
          <router-link to="/login" class="nav-link">Login</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/register" class="nav-link">Register</router-link>
        </li>
      </template>
    </ul>
  </nav>
</template>

<script>
import {computed} from 'vue';
import {useStore} from "vuex";
import axios from 'axios';
import {useRouter} from "vue-router";

export default {
  name: "Nav",
  setup() {
    const store = useStore();
    const router = useRouter();

    const auth = computed(() => store.state.auth);

    const logout = async () => {
      await axios.post('logout', {});

      await store.dispatch('setAuth', false);

      await router.push('/login');
    }

    return {
      auth,
      logout
    }
  }
}
</script>
