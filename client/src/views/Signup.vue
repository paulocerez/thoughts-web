<template lang="">
	<div class="flex min-h-full flex-1 flex-col justify-center px-6 py-12 lg:px-8 bg-green">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <img class="mx-auto h-20 w-auto" src="../assets/thoughts_logo.png" alt="Your Company" />
      <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-white-900">let's get to work - register now &lt3 </h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form @submit.prevent="signup" class="space-y-6">
        <div>
          <label for="username" class="block text-left text-sm font-medium leading-6 text-white-900">username</label>
          <div class="mt-2">
            <input id="username" name="username" type="text" v-model="username" required class="loginSignupInputs" />
          </div>
        </div>
        <div>
          <label for="email" class="block text-left text-sm font-medium leading-6 text-white-900">email address</label>
          <div class="mt-2">
            <input id="email" name="email" type="email" v-model="email" required class="loginSignupInputs" />
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
			  <label for="password" class="block text-left text-sm font-medium leading-6 text-white-900">password</label>
			  <div class="text-sm">
            </div>
          </div>
          <div class="mt-2">
            <input id="password" name="password" type="password" v-model="password" required class="loginSignupInputs" />
          </div>
        </div>

        <div>
          <button type="submit" class="loginSignupButton">create account</button>
        </div>
      </form>

      <p class="mt-10 text-center text-sm text-gray-500">
        Got one already?
        {{ ' ' }}
        <router-link to="/login" class="font-semibold leading-6 text-sky-600 hover:text-sky-400">Go to Login</router-link>
      </p>
    </div>
  </div>
  </template>
<script lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";
import axios from 'axios'
import config from "../../config"

const router = useRouter();

export default {

	data() {
		return {
			username: '',
			email: '',
			password: ''
		}
	},
	methods: {
		async signup() {
			try {
				await axios.post(`${config.apiUrl}/api/signup`, {
					username: this.username,
					email: this.email,
					password: this.password
				}, {
					headers: {
						'Content-Type': 'application/json'
					}
				})
				this.$router.push('/login');
			} catch (error) {
				alert('Signup failed. Seems you already have an account.');
			}
		}
	}
}

</script>
  