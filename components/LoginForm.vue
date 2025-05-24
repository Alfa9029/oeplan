//LoginForm.vue

<template>
  <div class="w-full max-w-sm bg-white shadow-md rounded-lg p-6">
    <h2 class="text-xl font-semibold text-center mb-4">Login</h2>
    <form @submit.prevent="handleSubmit">
      <div class="mb-4">
        <label class="block text-gray-700">Email</label>
        <input
          type="email"
          v-model="email"
          placeholder="name@example.com"
          class="w-full border rounded-md py-2 px-3 outline-none"
        />
      </div>
      <div class="mb-4 relative">
          placeholder="name@example.com"
          class="w-full border rounded-md py-2 px-3 outline-none"
        />
      </div>
      <div class="mb-4 relative">
          placeholder="name@example.com"
          class="w-full border rounded-md py-2 px-3 outline-none"
        />
      </div>
      <div class="mb-4 relative">
        <label class="block text-gray-700">Senha</label>
        <input
          :type="showPassword ? 'text' : 'password'"
          v-model="password"
          placeholder="••••••••"
          class="w-full border rounded-md py-2 px-3 outline-none"
        />
        <button
          type="button"
          @click="showPassword = !showPassword"
          class="absolute right-3 top-10"
        >
          <svg
            v-if="showPassword"
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 text-gray-400"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 12l-3 3-3-3m0-3l3-3 3 3m4 6a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
          <svg
            v-else
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 text-gray-400"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M13.875 18.825a10.05 10.05 0 01-3.75.675c-5 0-9.5-4-9.5-4s1.5-2.75 3.5-4.125m4-1.875A10.05 10.05 0 0112 5.25m4.5 4.875A9.982 9.982 0 0121 12s-4.5 4-9.5 4a10.05 10.05 0 01-3.75-.675"
            />
          </svg>
        </button>
        <a href="#" class="text-sm text-blue-500 absolute right-0 -bottom-5"
          >Esqueceu a senha?</a
        >
      </div>
      <button
        class="w-full bg-teal-800 text-white py-2 rounded-md mt-8 hover:bg-teal-700 transition duration-200"
      >
        Entrar
      </button>
      <p class="text-sm text-center text-gray-600 mt-4">
        Precisa de ajuda?
        <a href="#" class="text-teal-600">Entre em contato</a>
      </p>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const showPassword = ref(false)

function handleSubmit() {
  console.log('Email:', email.value)
  console.log('Senha:', password.value)
}
</script>
